# roobo OS

roobo OS是一套专为智能硬件设计的中间件。roobo OS能够通过标准化方式接入各类硬件。同时提供一整套应用开发服务，方便场景开发。roobo OS致力于缩短智能硬件的开发时间，同时能够更灵活的整合各种功能以及算法，提供用户需要的智能硬件。

roobo OS连接到roobo语义云和服务云，同时在本地集成了成熟的语音识别方案，也提供了场景调度及场景动画框架，打通了从用户语音到云端处理，再到本地展示的整体流程。在这套框架之上，用户可以编写自己的本地场景处理逻辑，快速实现功能。

针对不同的硬件设备，roobo OS也提供了一整套标准化接口，包含运动控制，触摸传感器和LED灯阵显示等。借助roobo OS的功能，用户可以快速支持新增设备，同时也能够借助标准化的接口将已有的功能顺利移植到新的硬件上。

<table>
  <tr>
    <td>分类</td>
    <td >实体名称</td>
    <td>实体描述</td>
    <td >举例</td>
    <td>返回数据格式</td>
  </tr>
  <tr>
    <td rowspan="2">时间</td>
    <td>sdate</td>
    <td>匹配日期</td>
    <td>明天，大后天明年三月四号，下个月五号国庆节等</td>
    <td>
      <div> {"year":"2017","month":"05",</div>
      <div>"day":"26","especial":"",</div>
      <div>"kind":0, "status":0,</div>
      <div>"leap":false,"delta":0,</div>
      <div>"yeardelta":0,"monthdelta":0}</div>
      <div>year :年</div>
      <div>month:月</div>
      <div>day:日</div>
      <div>especial：节日描述</div>
      <div>kind： 农历，公历</div>
      <div>status： 状态</div>
      <div>leap: 是否是闰月</div>
      <div>delta: 天数，做推理用（三十之后的100天，只支持天数)</div>
      <div>yeardelta:</div>
      <div>monthdelta:</div>
    </td>
  </tr>
  <tr>
    <td>datatime</td>
    <td>匹配一个日期时间(有明确日期概念时（三个小时之后，明天12点，12月23号上午7点45 等），给出日期+时间； 没有明确日期概念时（12点，下午两点），只给出时间。 只支持公历日期)</td><td>三个小时之后,下午两点</td>
    <td>{"date":"2017-01-01", "time":"08:00:00", "meridian":"am", "illegal":0}</td>
  </tr>
  <tr>
    <td rowspan="2">数字</td>
    <td>number</td>
    <td>数字</td>
    <td>一万零三十</td>
    <td>10030</td>
  </tr>
  <tr>
    <td>ordinal</td>
    <td>序数</td>
    <td>第8个</td>
    <td>8</td>
  </tr>
  <tr>
    <td rowspan="6">计量</td>
    <td>unit_area</td>
    <td>匹配面积(基准单位m2)</td>
    <td>1平方米</td>
    <td>{"amount":1,"unit":"m2"}</td></tr>
  <tr>
    <td>unit_currency</td>
    <td>匹配汇率(unit 是变化的 范围参考 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217))</td>
    <td>10美</td>
    <td>{"amount":10,"unit":"USD"}</td>
  </tr>
  <tr>
    <td>unit_lenght</td>
    <td>匹配长度(基准单位m)</td>
    <td>5厘米</td>
    <td>{"amount":0.05,"unit":"m"}</td>
  </tr>
  <tr>
    <td>unit_speed</td>
    <td>匹配速度(基准单位km/h)</td>
    <td>6千米每小时</td>
    <td>{"amount":6,"unit":"km/h"}</td>
  </tr>
  <tr>
    <td>unit_volume</td>
    <td>匹配体积(基准单位l)</td>
    <td>890毫升</td>
    <td>{"amount":0.89,"unit":"l"}</td>
  </tr>
  <tr>
    <td>unit_weight</td>
    <td>匹配重量(基准单位g)</td>
    <td>9斤</td
    <td>{"amount":4500,"unit":"g"}</td>
  </tr>
  <tr>
    <td rowspan="4">地理信息</td>
    <td>geog_country</td>
    <td>国家</td>
    <td>不丹</td>
    <td>不丹</td>
  </tr>
  <tr>
    <td>geog_province</td>
    <td>中国省份</td>
    <td>河南省</td>
    <td>河南省</td>
  </tr>
  <tr>
    <td>geog_city</td>
    <td>中国地级城市及以上城市</td>
    <td>北京市</td>
    <td>北京市</td>
  </tr>
  <tr>
    <td>geog_district</td>
    <td>中国区/县</td>
    <td>朝阳区</td>
    <td>朝阳区</td>
  </tr>
  <tr>
    <td rowspan="2">通用匹配</td>
    <td>any</td>
    <td>匹配任何字符或者空。同一模板中优先级最低，先匹配其他槽位。</td>
    <td>打电话给@sys.any:name打电话给李XXX</td>
    <td></td>
  </tr>
  <tr>
    <td>default</td>
    <td>在模板中单独使用，需要配置上文,匹配任何字符。</td>
    <td>例如：英译汉场景。进入场景后，只要没有退出场景，所有后面的输入都需要翻译。就需要在场景中配置一个只有default的模板来匹配所有的输入，来实现这个功能。</td>
    <td></td>
  </tr>
</table>
