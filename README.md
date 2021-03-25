# Knowledge-points-elsewhere

-居中详解 http://ife.baidu.com/note/detail/id/1549

# json对象的null值处理，转成空字符串""，输出json字符串
```
var settings = new JsonSerializerSettings() { ContractResolver= new NullToEmptyStringResolver() };
var str = JsonConvert.SerializeObject(yourObj, settings);
```
```
public class NullToEmptyStringResolver : Newtonsoft.Json.Serialization.DefaultContractResolver
{
    protected override IList<JsonProperty> CreateProperties(Type type, MemberSerialization memberSerialization)
    {
        return type.GetProperties()
                .Select(p=>{
                    var jp = base.CreateProperty(p, memberSerialization);
                    jp.ValueProvider = new NullToEmptyStringValueProvider(p);
                    return jp;
                }).ToList();
    }
}

public class NullToEmptyStringValueProvider : IValueProvider
{
    PropertyInfo _MemberInfo;
    public NullToEmptyStringValueProvider(PropertyInfo memberInfo)
    {
        _MemberInfo = memberInfo;
    }

    public object GetValue(object target)
    {
        object result =  _MemberInfo.GetValue(target);
        if (_MemberInfo.PropertyType == typeof(string) && result == null) result = "";
        return result;

    }

    public void SetValue(object target, object value)
    {
        _MemberInfo.SetValue(target, value);
    }
}
```
# json字符串转实体类忽略null值
```
var jsonSetting = new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore };
```
