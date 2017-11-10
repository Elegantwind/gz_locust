## locust压测
    其实很简单主要运行的任务就在locustfle.py中。
    单独的时候命令运行时: locust -f locustfile.py --host=http://api.kikakeyboard.com
    作为Master机运行时: locust -f locustfile.py --master --host=http://api.kikakeyboard.com
    作为Slave机运行时: locust -f locustfile.py --slave --master-host=对应maser ip
    Dockerfile中是对应docker的一些配置信息
    requirements.txt中是Python依赖
## 用例格式
    格式：
    url: https://api.kikakeyboard.com/v1/utils/get_app_config?key=sticker2&
    拼接到url中的key值(duid=sign)
    keys: 'duid' keys
    对应的data数据
    data:
    app对应值必填(给header用至少1个)
        app: ['kika','ikey','pro']
    kb_lang=lang必填(给header用至少1个)
        kb_lang : ['en_US', 'en_AU', 'es_AR', 'pt_BR', 'in_ID']
    duid必填(给header用至少1个)
        duid : ['5a215835df204115ee3d2d4ec0c528aa', 'adad79631d9339915e3be1c9e783e82d', 'a2bb5434f3541bf5aa64186ec8c2b77f','920b56e9cadd743bfbbcb4126937e789']
    检查点
    assert:
    返回码(只能第一层)
        code : {'key':'errorCode','value':0}
    字段格式
        data_format : {"errorCode":'Str',"errorMsg":'Str',"data":{'tag':'&&&'}}
    数据检查
        data_content : { 'es&adad79631d9339915e3be1c9e783e82d&kika':"'popupdelay': 500", 'es&a2bb5434f3541bf5aa64186ec8c2b77f&kika':"'popupdelay': 400", 'es&920b56e9cadd743bfbbcb4126937e789&kika':"'popupdelay': 600" }
    其他内容设定
    other:
    版本号
        version: 2043
    header的选择(其实就是api或api-dev)
        way: online
    host填写(针对非api.kika和api-dev.kika)
        host:
