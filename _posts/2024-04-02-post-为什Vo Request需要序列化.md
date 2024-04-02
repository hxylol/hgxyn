# 为什Vo Request需要序列化

```java
/**
 * <p>
 * 角色查询实体
 * </p>
 *
 * @author qy
 * @since 2019-11-08
 */
public class SysRoleQueryVo implements Serializable {
 
 private static final long serialVersionUID = 1L;
 
 private String roleName;

 public String getRoleName() {
  return roleName;
 }

 public void setRoleName(String roleName) {
  this.roleName = roleName;
 }
}
```

## 一、序列化的含义、意义及使用场景

- **序列化：将对象写入到IO流中**
- **反序列化：从IO流中恢复对象**
- **意义：序列化机制允许将实现序列化的Java对象转换位字节序列，这些字节序列可以保存在磁盘上，或通过网络传输，以达到以后恢复成原来的对象。序列化机制使得对象可以脱离程序的运行而独立存在。**
- **使用场景：所有可在网络上传输的对象都必须是可序列化的，**比如RMI（remote method invoke,即远程方法调用），传入的参数或返回的对象都是可序列化的，否则会出错；**所有需要保存到磁盘的java对象都必须是可序列化的。通常建议：程序创建的每个JavaBean类都实现Serializeable接口。**

### 四、总结

1. 所有需要网络传输的对象都需要实现序列化接口，通过建议所有的javaBean都实现Serializable接口。
2. 对象的类名、实例变量（包括基本类型，数组，对其他对象的引用）都会被序列化；方法、类变量、transient实例变量都不会被序列化。
3. 如果想让某个变量不被序列化，使用transient修饰。
4. 序列化对象的引用类型成员变量，也必须是可序列化的，否则，会报错。
5. 反序列化时必须有序列化对象的class文件。
6. 当通过文件、网络来读取序列化后的对象时，必须按照实际写入的顺序读取。
7. 单例类序列化，需要重写readResolve()方法；否则会破坏单例原则。[https://juejin.cn/post/6854573210495631374?searchId=20240227102739B4D5AE3DE08FA9C69B73](https://juejin.cn/post/6854573210495631374?searchId=20240227102739B4D5AE3DE08FA9C69B73)
8. 同一对象序列化多次，只有第一次序列化为二进制流，以后都只是保存序列化编号，不会重复序列化。
9. 建议所有可序列化的类加上serialVersionUID 版本号，方便项目升级。
