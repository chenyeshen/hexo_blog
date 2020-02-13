---
layout:     post
title:      Dubbo整合SpringBoot
subtitle:   学习笔记
date:       2019-08-28
author:     chenyeshen
header-img: img/img2.jpg
catalog: true
tags:
    - Springboot
    - Dubbo
---

## 一、引入依赖

```
  <!-- dubbo依赖 -->
  <dependency>
       <groupId>com.alibaba.boot</groupId>
       <artifactId>dubbo-spring-boot-starter</artifactId>
       <version>0.2.0</version>
   </dependency>

```

## 二、创建服务提供者springboot-service-provider

### 1、创建实体UserAddress

```
/**用户地址*/
public class UserAddress implements Serializable {
	
	private Integer id;
    private String userAddress; //用户地址
    private String userId; //用户id
    private String consignee; //收货人
    private String phoneNum; //电话号码
    private String isDefault; //是否为默认地址    Y-是     N-否
    
    public UserAddress() {
		super();
	}
    
	public UserAddress(Integer id, String userAddress, String userId, String consignee, String phoneNum,
                       String isDefault) {
		super();
		this.id = id;
		this.userAddress = userAddress;
		this.userId = userId;
		this.consignee = consignee;
		this.phoneNum = phoneNum;
		this.isDefault = isDefault;
	}
	
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getUserAddress() {
		return userAddress;
	}
	public void setUserAddress(String userAddress) {
		this.userAddress = userAddress;
	}
	public String getUserId() {
		return userId;
	}
	public void setUserId(String userId) {
		this.userId = userId;
	}
	public String getConsignee() {
		return consignee;
	}
	public void setConsignee(String consignee) {
		this.consignee = consignee;
	}
	public String getPhoneNum() {
		return phoneNum;
	}
	public void setPhoneNum(String phoneNum) {
		this.phoneNum = phoneNum;
	}
	public String getIsDefault() {
		return isDefault;
	}
	public void setIsDefault(String isDefault) {
		this.isDefault = isDefault;
	}

}


```

### 2、创建接口UserService

```
/**用户服务*/
public interface UserService {
	
	/**
	 * 按照用户id返回所有的收货地址
	 * @param userId
	 * @return
	 */
	public List<UserAddress> getUserAddressList(String userId);

}

```

### 3、创建UserService接口的实现类UserServiceImpl

```
@Service //使用com.alibaba.dubbo.config.annotation.Service注解。暴露服务
@Component
public class UserServiceImpl implements UserService {

	@Override
	public List<UserAddress> getUserAddressList(String userId) {
		UserAddress address1 = new UserAddress(1, "北京市昌平区宏福科技园综合楼3层", "1", "李老师", "010-56253825", "Y");
		UserAddress address2 = new UserAddress(2, "深圳市宝安区西部硅谷大厦B座3层（深圳分校）", "1", "王老师", "010-56253825", "N");

		if(Math.random()>0.5){
			throw new RuntimeException();
		}
		return Arrays.asList(address1,address2);
	}
}

```

### 4、在application.properties配置dubbo

```
dubbo.application.name=springboot-service-provider
dubbo.registry.address=127.0.0.1:2181
dubbo.registry.protocol=zookeeper

dubbo.protocol.name=dubbo
dubbo.protocol.port=20881

dubbo.monitor.protocol=registry

```

### 5、在主程序中开启dubbo功能

```
@EnableDubbo //开启基于注解的dubbo功能
@SpringBootApplication
public class SpringbootServiceProviderApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootServiceProviderApplication.class, args);
    }

}

```

## 三、创建服务消费者springboot-service-consumer

### 1、创建OrderController

```
@Controller
public class OrderController {

    @Autowired
    OrderService orderService;

    @ResponseBody
    @RequestMapping("/initOrder")
    public List<UserAddress> initOrder(@RequestParam("uid") String userId){
        return orderService.initOrder(userId);
    }
}

```

### 2、创建接口OrderService

```
public interface OrderService {

    /**
     * 初始化订单
     * @param userId
     */
    public List<UserAddress> initOrder(String userId);
}

```

### 3、创建接口OrderService 的实现类OrderServiceImpl

```
/**
 * 1、将服务提供者注册到注册中心
 *    1）、导入dubbo依赖（2.6.2）、操作zookeeper的客户端(curator)
 *    2）、配置服务提供者
 * 2、让服务消费者去注册中心订阅服务提供者的服务地址
 */
@Service
public class OrderServiceImpl implements OrderService {

    @Reference //使用com.alibaba.dubbo.config.annotation.Reference注解。远程调用服务
    UserService userService;

    @Override
    public List<UserAddress> initOrder(String userId) {
        System.out.println("用户id："+userId);
        //1、查询用户的收货地址
        List<UserAddress> userAddressList = userService.getUserAddressList(userId);
        return userAddressList;
    }
}

```

### 4、在application.properties配置dubbo

```
dubbo.application.name=springboot-service-consumer
dubbo.registry.address=zookeeper://127.0.0.1:2181
dubbo.monitor.protocol=registry

```

### 5、在主程序中开启dubbo功能

```
@EnableDubbo //开启基于注解的dubbo功能
@SpringBootApplication
public class SpringbootServiceConsumerApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootServiceConsumerApplication.class, args);
    }

}

```

### 6、测试远程调用提供者

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190427185957836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpemhpcWlhbmcxMjE3,size_16,color_FFFFFF,t_70)
