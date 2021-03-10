
        
        ```
        //扩展方法 获取毫秒级13位时间戳
        public static string ToTimeStampOfMileSeconds(this DateTime dt)
        {
            DateTime dateStart = TimeZoneInfo.ConvertTime(new DateTime(1970, 1, 1), TimeZoneInfo.Utc, TimeZoneInfo.Local);
            string timeStamp = (dt.Ticks - dateStart.Ticks).ToString().Substring(0, 13);
            return timeStamp;
        }
        ```
        
        ```
        //扩展方法 获取秒级10位时间戳
        public static string ToTimeStampOfSeconds(this DateTime dt)
        {
            DateTime dateStart = TimeZoneInfo.ConvertTime(new DateTime(1970, 1, 1), TimeZoneInfo.Utc, TimeZoneInfo.Local);
            string timeStamp = (dt.Ticks - dateStart.Ticks).ToString().Substring(0, 10);
            return timeStamp;
        }
        ```
