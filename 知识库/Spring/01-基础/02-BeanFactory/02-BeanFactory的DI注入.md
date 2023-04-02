**定义UserDao接口及其UserDaoImpl实现类**
```java
public interface UserDao {
    
}

public class UserDaoImpl implements UserDao {

}
```
**修改UserServiceImpl代码，添加一个setUserDao(UserDao userDao)用于接收注入的对象**
```java
public class UserServiceImpl implements UserService {
    public UserDao userDao;

    // BeanFactory去调用该方法，从容器中获取userDao设置到此
    public void setUserDao(UserDao userDao) {
        System.out.println("BeanFactory去调用该方法获取userDao设置到此处："+userDao);
        this.userDao = userDao;
    }
}
```

**修改beans.xml配置文件，在UserDaoImpl的<Bean>中嵌入<property>配置注入**
```xml
<!--配置UserServiceImpl-->
<bean id="userService" class="com.kafe.service.impl.UserServiceImpl">
    <property name="userDao" ref="userDao"></property>
</bean>

<!--配置UserDaoImpl-->
<bean id="userDao" class="com.kafe.dao.impl.UserDaoImpl"></bean>
```
**修改测试代码，获得UserService时，setUserService方法执行了注入操作**
```java
public class BeanFactoryTest {
    public static void main(String[] args) {
        // 创建工厂对象
        DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();
        // 创建一个xml读取器
        XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(beanFactory);
        // 读取配置文件给工厂
        reader.loadBeanDefinitions("beans.xml");

        // 根据id获取bean对象
        UserService userService = (UserService) beanFactory.getBean("userService");
        System.out.println(userService);
    }
}
```
