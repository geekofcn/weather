<h1 align="center"> weather </h1>

<p align="center"> 基于 <a href="https://lbs.amap.com/dev/id/newuser">高德开放平台</a> 的 PHP 天气信息组件。</p>


## 安装

```shell
$ composer require geekofcn/weather -vvv
```
## 配置
在使用本扩展之前，你需要去 高德开放平台 注册账号，然后创建应用，获取应用的 API Key。

## 使用
```shell
use Geekofcn\Weather\Weather;

$key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx';

$weather = new Weather($key);
```
### 获取实时天气
```shell
$response = $weather->getWeather('北京');
```
结果
```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "北京",
            "city": "北京市",
            "adcode": "110000",
            "weather": "多云",
            "temperature": "18",
            "winddirection": "西",
            "windpower": "≤3",
            "humidity": "53",
            "reporttime": "2020-04-19 18:58:35"
        }
    ]
}
```
### 获取近期天气预报
```php
$response = $weather->getWeather('北京', 'all');
```
结果
```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "forecasts": [
        {
            "city": "北京市",
            "adcode": "110000",
            "province": "北京",
            "reporttime": "2020-04-19 18:58:35",
            "casts": [
                {
                    "date": "2020-04-19",
                    "week": "7",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "21",
                    "nighttemp": "10",
                    "daywind": "西南",
                    "nightwind": "西南",
                    "daypower": "4",
                    "nightpower": "4"
                },
                {
                    "date": "2020-04-20",
                    "week": "1",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "16",
                    "nighttemp": "4",
                    "daywind": "西北",
                    "nightwind": "西北",
                    "daypower": "5",
                    "nightpower": "5"
                },
                {
                    "date": "2020-04-21",
                    "week": "2",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "16",
                    "nighttemp": "4",
                    "daywind": "西北",
                    "nightwind": "西北",
                    "daypower": "5",
                    "nightpower": "5"
                },
                {
                    "date": "2020-04-22",
                    "week": "3",
                    "dayweather": "晴",
                    "nightweather": "晴",
                    "daytemp": "17",
                    "nighttemp": "5",
                    "daywind": "北",
                    "nightwind": "北",
                    "daypower": "5",
                    "nightpower": "5"
                }
            ]
        }
    ]
}
```
### 获取XML格式的返回值
```php
$response = $weather->getWeather('北京', 'all', 'xml');
```
结果
```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
<status>1</status>
<count>1</count>
<info>OK</info>
<infocode>10000</infocode>
<lives type="list">
<live><province>北京</province>
<city>北京市</city>
<adcode>110000</adcode>
<weather>多云</weather>
<temperature>18</temperature>
<winddirection>西</winddirection>
<windpower>≤3</windpower>
<humidity>53</humidity>
<reporttime>2020-04-19 18:58:35</reporttime>
</live></lives>
</response>
```
### 参数说明
array|string getWeather(string $city, string $type = 'base', string $format = 'json')
> - $city - 城市名，比如：“北京”；
> - $type - 返回内容类型：base: 返回实况天气 / all: 返回预报天气；
> - $format - 输出的数据格式，默认为 json 格式，当 output 设置为 “xml” 时，输出的为 XML 格式的数据。
### 在 Laravel 中使用
配置写在 config/services.php 中，添加：
```php
'weather' => [
        'key' => env('WEATHER_API_KEY'),
    ],
```
然后在 .env 中配置 WEATHER_API_KEY ：
```.dotenv
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxxxxx
```
方法参数注入
```php
 public function edit(Weather $weather) 
 {
     $response = $weather->getWeather('北京');
 }
```
服务名访问
```php
public function edit() 
{
   $response = app('weather')->getWeather('北京');
}
```

## 参考
- <a href="https://lbs.amap.com/api/webservice/guide/api/weatherinfo/">高德开放平台天气接口</a>
## Contributing

You can contribute in one of three ways:

1. File bug reports using the [issue tracker](https://github.com/geekofcn/weather/issues).
2. Answer questions or fix bugs on the [issue tracker](https://github.com/geekofcn/weather/issues).
3. Contribute new features or update the wiki.

_The code contribution process is not very formal. You just need to make sure that you follow the PSR-0, PSR-1, and PSR-2 coding guidelines. Any new code contributions must be accompanied by unit tests where applicable._

## License

MIT