# roobo OS

roobo OS是一套专为智能硬件设计的中间件。roobo OS能够通过标准化方式接入各类硬件。同时提供一整套应用开发服务，方便场景开发。roobo OS致力于缩短智能硬件的开发时间，同时能够更灵活的整合各种功能以及算法，提供用户需要的智能硬件。

roobo OS连接到roobo语义云和服务云，同时在本地集成了成熟的语音识别方案，也提供了场景调度及场景动画框架，打通了从用户语音到云端处理，再到本地展示的整体流程。在这套框架之上，用户可以编写自己的本地场景处理逻辑，快速实现功能。

针对不同的硬件设备，roobo OS也提供了一整套标准化接口，包含运动控制，触摸传感器和LED灯阵显示等。借助roobo OS的功能，用户可以快速支持新增设备，同时也能够借助标准化的接口将已有的功能顺利移植到新的硬件上。

<table>
    <tr>
        <td>Category</td>
        <td >Name</td>
        <td>Descript</td>
        <td>Explame</td>
        <td>Data</td>
    </tr>
    <tr>
        <td rowspan="2">时间</td>
        <td>sdate</td>
        <td>匹配日期</td>
        <td>明天，大后天明年三月四号，下个月五号国庆节等</td>
        <td>
            {"year":"2017","month":"05","day":"26","especial":"",
            "kind":0,"status":0,"leap":false,"delta":0,"yeardelta":0,"monthdelta":0}
            type SDate struct {
            Year string `json:"year"` // 十二生肖，所以是string
            Month string `json:"month"` // 与year保持一致
            Day string `json:"day"` // 与year保持一致
            Especial string `json:"especial"` // 三十儿,二十四节气啥的，每年不确定是哪一天的
            Kind LunisolarCalendar `json:"kind"` // 农历，公历
            Status SysFuncStatusCode `json:"status"` // 状态
            LeapMonth bool `json:"leap"` // 是否是闰月
            Delta int `json:"delta"` //天数，做推理用（三十之后的100天，只支持天数）。 因为农历每个月的日子不固定，service自己算
            YearDelta int `json:"yeardelta"` // 例：下一个猴年，yeardelta：12， 上一个猴年: yeardelta: -1
            MonthDelta int `json:"monthdelta"` //例：三个月后的初一，因为是阴历，所以这个月是几月框架没有概念。
            }
        </td>
    </tr>
    <tr>
        <td>datatime</td>
        <td>匹配一个日期时间</td><td>三个小时之后,下午两点</td>
        <td>有明确日期概念时（三个小时之后，明天12点，12月23号上午7点45 等），给出日期+时间； 没有明确日期概念时（12点，下午两点），只给出时间。 只支持公历日期</td>
    </tr>
</table>
