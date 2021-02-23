# JVM注入动态脚本

向指定的Java方法注入一段动态代码，您可通过代码方式实施任意故障场景，例如篡改方法入参、篡改方法返回值等。

参数说明如下：

|参数名称|是否必选|默认值|参数说明|
|----|----|---|----|
|脚本类型|否|Java|动态脚本的语言类型，可选项：Java、Groovy。|
|脚本名称|否|无|动态脚本的名称。|
|脚本内容|是|无|动态脚本的代码。|
|类名|是|无|完整的类名，包含报名。例如：com.alibaba.service.XxxService。如果模拟接口故障，需填写接口的实现类。|
|方法名|是|无|方法名，例如：方法getUser\(Long userId\)，则填写getUser。如果存在多个重载方法，如：getUser\(String name\) 和getUser\(Long userId\)，则对两个方法均生效。|
|返回值|是|无|指定方法的期望返回值，仅支持基础类型、基础类型的包装类、String类型。如果返回空值，填写null。|
|进程关键字|必选其一|无|用于识别唯一的关键字，可以通过该关键字查找到唯一进程，使用`ps -ef | grep <key>`来尝试查找进程，能找到唯一进程则正确。|
|进程ID|无|进程的ID。|
|受影响的请求数|否|0|限制最多发生故障的请求总数，每生效一次故障计数加1，累计发生故障请求数超出设定值后，请求则不再发生故障。填写数值小于等于0时，则表示不限制。|
|受影响的请求占比（%）|否|0|限制发生故障的请求数占所有应该发生故障请求数的百分比，也可代表每次请求发生故障的概率。填写小于或等于0，则表示100% 发生故障。**说明：** 仅填写百分比数字部分即可，即80%，填写80。 |
|请求过滤规则|否|无|通过脚本方式自定义规则，通过自定义规则决策是否对请求产生故障。自定义规则生效前提为需满足其它设定条件。|
|过滤规则执行阶段|否|无|自定义过滤规则执行的阶段，可选择Java方法调用前执行或Java方法调用后执行。|
|开启Debug|否|false|选择是否开启Debug日志，用于排查演练执行过程中遇到的问题。开启Debug后，请到`~/logs/chaosblade/chaosblade.log`路径下查看日志。|

## 脚本编写说明（以Java为例）

被故障注入代码：

```
package com.alibaba.service; 

import com.aliaba.model.UserDO; 

public class UserService {

    private UserMapper userMapper;

    public UserDO getUserById(Long userId) { 
        UserDO user = userMapper.findUser(userId);
        return user;
    } 
}
```

注入的脚本代码：示例脚本演示通过自定义脚本方式篡改方法返回值。

```
// 需要创建类，并import需要的类。
// 如果import自定义类，需要保证该类在目标应用系统中存在。import java.util.Map;
import com.aliaba.model.UserDO;

public class UserServiceInterceptor {

    // 必须包含该方法，且该方法的定义不可改变(返回值、类名、参数均不可改变)。 
    // 参数context包含的内容参⻅《脚本入参说明》。public Object run(Map<String, Object> context) {
        //获取getUserById方法的实际入参 
        //Map的key是getUserById方法的参数列表的索引位置，value是参数值Map<Integer, Object> arguments = context.get("params");

        //获取getUserById方法的一个参数，即userId 
        Long userId = (Long)arguments.get(0);

        //构建篡改后的方法返回值UserDO mockUser = new UserDO(); 
        mockUser.setUserId(userId); //使用真实的userId 
        mockUser.setUserName("mock_user_name"); //构造错误的userName

        //返回篡改后的对象return mockUser;
    }

}
```

脚本入参说明：

**说明：** 列表中的对象可通过conext.get\(key\) 获得。例如：key为object，即通过context.get\("object"\) 获得。

|key|描述|返回值类型|
|params|方法的参数列表|java.util.Map<Integer,Object\>（Map的key为拦截的方法的参数列表中参数的索引值，value为参数取值）|
|object|调用方法的应用对象|实际拦截的类的实例|
|method|当前调用方法的实例|java.lang.reflect.Method|
|return|实际的返回值（仅“选择生效阶段”填写true时有效）|实际拦截的方法的返回|

日志输出：

使用slf4j打印日志。

```
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

Logger logger = LoggerFactory.getLogger("logger_name");
```

