# Knowledge-points-elsewhere


# 数据库表字段='NULL'和 is null注意区别，尤其复制表后

# 居中详解 http://ife.baidu.com/note/detail/id/1549

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
# 递归查询
可以查询后，再对递归的表进行操作，但是有时候将递归表放在join中会特别慢，可以将值取出来放到临时表中

```

   if object_id('tempdb..#tempTable') is not null
   begin  drop table #tempTable  end;
   with cte as(select ID from T1 where parentID='1' union all select T1.ID from position inner join subs on T1.parentID=cte.positionID)
   select T2.XX into #tempTable from T2  right join cte t2 on t1.XXID=t2.ID
```
# 按XXID排序后添加一列自增列
```
   select *,ROW_NUMBER()over(partition by XXID order by Time desc )as xx_index  from T1
```
# 获取表单中所有textbox
```
 foreach (Control control in this.Page.FindControl("form1").Controls)
            {
                if (control is TextBox textBox)
                {
                    //判断非空的textbox的值是否为整数
                    if (textBox.ID.Contains("amount") && !string.IsNullOrEmpty(textBox.Text) && !int.TryParse(textBox.Text, out int temp))
                    {
                        Response.Write("<script>alert('请输入正确的数字')</script>");
                        return false;
                    }
                }
            }
```
# window.showModalDialog 兼容方法
https://github.com/niutech/showModalDialog
