ApplicationContext称为Spring容器，内部封装了BeanFactory，比BeanFactory功能更丰富更强大，使用ApplicationContext进行开发时，xml配置文件的习惯写成applicationContext.xml
```java
public class ApplicationContextTest {
    public static void main(String[] args) {
        // 创建ApplicationContext，加载配置文件，实例化容器
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        // 根据beanName获得容器中的Bean实例
        UserService userService = (UserService) context.getBean("userService");
        System.out.println(userService);
    }
}
```
