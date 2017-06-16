# Video-Api documentation
All Ids ll be deleted/hidden from all endpoints, so to identify a particular ressource, developers should use ckey(channel key), vkey(video key), pkey(playlist key), no need for ukey, because jwt token already include it

**Path**: GET /video/get => cache duration 20min

**Params**: lang=fr/en/ar; vkey=XXX => video key, pkey=xxx playlist key (optional)

>Desc: `Fetch video content`

>400(means video not found) & 500 erros should be captured

**Result**:

```json
{
"status": 1,
"video":{
"vtitle": "واش فراسك..لهذه الأسباب تجنبوا معطرات الجو",
"ch_title": "Chouf TV | شوف تيفي",
"avatar": "1",
"verified": "1",
"subscribers_count": "5,651",
"vast_ad_tag": "",
"link": "https://d3ll6wq5wpnvvt.cloudfront.net",
"default_lang": "ar",
"description": "مما لا شك فيه أن استخدام المعطرات الجوية بصوره مستمرة فى الكثير من المنازل حول العالم ان لم يكن جميع المنازل حول العالم وتستخدم المعطرات لتعطير الجو داخل المنزل ، ان تلك المعطرات الجوية تقوم بدورها على امتصاص الروائح الكريهة في الجو سواء فى العمل او المنازل لتلطيف الجو وجعل الجو معطر وجيد ، ولكن هذه المواد العضوية المتطايرة تعمل على الأضرار بالجهاز التنفسي بصورة كبيرة إذا استخدمت أكثر من مره.",
"publish_datetime": "2017-03-31 11:44:47",
"comments": "0",
"ctitle": "Entertainment",
"ltitle": "Standard ChoufTV license",
"duration": "01:53",
"likes": "1",
"dislikes": "0",
"views": "52",
"ckey": "MQ",
"publish_time": "depuis à peu près un mois"
},
"CHANNEL_SMALL_AVATAR": "channels/avatars/small/",
"CDN": "https://cdn.choufplus.com/",
"related_videos":[
{"vtitle": "حسناء أبو زيد لشوف تيفي: لا نقبل أن ننخرط في منهيجة لا تجيب على واقع التراجع التمثيلي المجتمعي ",
"relevance": "2.966050148010254",
"ch_title": "Chouf TV | شوف تيفي",
"link": "https://cdn.choufplus.com",
"default_lang": "ar",
"duration": "01:25",
"views": "151",
"vkey": "MTND",
"ckey": "MQ"
},{"vtitle": "\u202bبعد سنة مفتاح لشوف تيفي-قبلت نجسد دور اليهودي في فيلم عادل إمام باش نْحبب الناس فاليهود\u202c", "relevance": "2.966050148010254", "ch_title": "Chouf TV | شوف تيفي",…},
{"vtitle": "تيحيحيت ترد بقوة على الفيديو الجنسي الشهير بدموع مؤثرة وتقرر مقاضاة من روج لهذه الشائعات", "relevance": "4.093550682067871", "ch_title": "Chouf TV | شوف تيفي",…},
{"vtitle": "نسولو الناس: واش تقدرو تعيشو بلا واتساب؟؟؟ أجوبة طريفة", "relevance": "4.093550682067871", "ch_title": "Chouf TV | شوف تيفي",…},
{"vtitle": "المخرج و الممثل ادريس الروخ يُهنئ شوف تيفي على 13 مليون متابع", "relevance": "7.059600830078125", "ch_title": "Chouf TV | شوف تيفي",…},
{"vtitle": "معاناة حقيقية للطبقة الشغيلة لحظة الاحتفال بعيد الشغل", "relevance": "7.059600830078125", "ch_title": "Chouf TV | شوف تيفي",…}
],
"comments":[
{
"ukey": "7f0ab833a33966e07c54ed91ba33cb18",
"name": "funny video",
"avatar": "1",
"datetime": "depuis 10 jours",
"text": "vfqvfqjvsfjvqs",
"cmkey": "QQ"
},
{"ukey": "7f0ab833a33966e07c54ed91ba33cb18", "name": "funny video", "avatar": "1", "datetime": "depuis 10 jours",…}
]
}
```
**Path**: POST /video/comment

**Params**:  vkey=xxx => video key, text=xxx => comment, , jwt token => header auth

>Desc: `comment a video`

>400 & 500 erros should be captured

**Result**:
```json
{
"status": 1
}
```

**Path**: GET /video/like

**Params**:  vkey=xxx => video key, type=0/1 => 0:dislike, 1:like, , jwt token => header auth

>Desc: `like a video`

>400 & 500 erros should be captured

**Result**:
```json
{
"status": 1/0,  => 0 if already liked or disliked
 "already_eval": 0/1 => 0 if already liked or disliked
}
```

**Path**: GET /video/sync

**Params**:  vkey=xxx => video key, jwt token => header auth

>Desc: `sync a video`

>400 & 500 erros should be captured

**Result**:
```json
{
"status": 1,
 "sync":{
  "subscribed": 1/0,
  "liked": 1/0,
  "disliked": 1/0,
 }
}
```

**Path**: POST /video/event

**Params**:  vkey=xxx => video key,
key:xxxx => event key(HEXA(timestamp) + ';' + 
event_type(enum => 'play_event', 'click_ad', 'startAds_event', 'endAds_event', 'aderr_503', 'aderr_1009', 'aderr_1012', 'aderr_unknown') ),
jwt token => header auth

>Desc: `Video event`

>400 & 500 erros should be captured

**Result**:
```json
{
"status": 1
}
```

**Path**: GET /video/report

**Params**:  vkey=xxx => video key, jwt token => header auth => will be update during next month for a better reporting form

>Desc: `report a video`

>400 & 500 erros should be captured

**Result**:
```json
{
"status": 1
}
```

**Path**: GET /video/infos

**Params**: lang=fr/en/ar => it's for publish_time formating, vkey=xxx => video key

>Desc: `Fetch video's informations`

>400 & 500 erros should be captured

**Result**:
web specific


**Path**: POST /video/edit

**Params**:  vkey=xxx => video key

>Desc: `Edit video infos`

>400 & 500 erros should be captured

**Result**:
web specific

**Path**: DELETE /video/delete

**Params**:  vkey=xxx => video key

>Desc: `delete video`

>400 & 500 erros should be captured

**Result**:
web specific

