---
layout: post
title: 客户端身份认证
date: 2015-8-17 17:17:02
author: VERYYOUNG
comments: true
categories: [Http]
---

浏览器端有cookie这个概念，能够很方面的保存客户端的状态，在cookie中保存sessionId，在客户端每次请求的时候都把这个sessionId带上，去和服务端的session对比，如果能匹配，则验证通过，返回登录状态下应该返回的页面。

搬到客户端来这一套就不好使了。因为客户端每个请求都是无状态的，服务端没法识别该请求来自哪个用户。

<!-- more -->

思路很简单，伪造一个类似cookie的东西，客户端每次请求都带上。一般情况下这东西叫做token。


----------
接口如下：



	public interface TokenService {
	
	
	    /**
	     * 判断token是否有效
	     *
	     * @param token
	     * @return
	     */
	    public boolean checkToken(String token);
	
	
	    /**
	     * 登陆成功后，存储token 并返回token
	     */
	    public String storeToken(String userId);
	
	
	    /**
	     * 登出
	     */
	    public void logout(String token);
	
	}


很简单的一个定义。

实现：

	@Service
	public class TokenServiceImpl extends BaseService implements TokenService {
	
	
	    @Autowired
	    private RedisService redisService;
	
	
	    @Override
	    public boolean checkToken(String token) {
	        if (StringUtils.isEmpty(token)) {
	            return false;
	        }
	
	        token = EncryptConverter.getOriginToken(URLDecoder.decode(token));
	
	        if (!token.contains("|")) {
	            return false;
	        }
	
	        String[] strings = token.split("\\|");
	
	        String userId = strings[0];
	
	        long timestamp = Long.parseLong(strings[1]);
	
	
	        String storedToken = redisService.get(userId);
	
	        if (StringUtils.isEmpty(storedToken)) {
	            return false;
	        }
	
	        if (!storedToken.equals(token)) {
	            return false;
	        }
	
	        long timeBetwwen = new Date().getTime() - timestamp;
	
	        if (timeBetwwen > 3600000) {
	            redisService.set(userId, token, 1800);
	        }
	        return true;
	    }
	
	    @Override
	    public String storeToken(String userId) {
	        String token = userId + "|" + new Date().getTime();
	        logger.debug("store {} in redis for user {}", token, userId);
	        redisService.set(userId, token, 1800);
	        return URLEncoder.encode(EncryptConverter.getEncodedToken(token));
	    }
	
	    @Override
	    public void logout(String token) {
	        redisService.del(TokenUtils.getUserIdFromToken(token));
	    }
	}






----------

解释：

----------

生成token：客户端发送用户名和密码，判断账户密码是否正确,如果正确，调用tokenService.storeToken(userId)来生成一个token，并把该token保存在redis中，同时返回给client。

token的规则是 	

	userId|timeStamp

返回给client的token需要进行des加密，并且urlEncode

token的有效时间为半小时




校验token：通过tokenService.checkToken(token)来校验token是否有效。

校验规则：先逆向token，得到userId和timeStamp，通过userId去获取存在redis中的token，对比两个token，同时还要对比两个timeStamp的时间间隔是否在30分钟以内，满足所有条件才算认证成功。在认证成功的情况下更新token有效期。


获取userId：TokenUtils.getUserIdFromToken（token）来得到对应token的userId

	public class TokenUtils {
	
	    public static String getUserIdFromToken(String token) {
	        return EncryptConverter.getOriginToken(URLDecoder.decode(token)).split("\\|")[0];
	    }
	}






