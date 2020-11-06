# Ranked-Retrieval-Model
有关实验二的相关实验报告以及代码实现
## 实验内容
在 Homework 1.1的基础上实现最基本的 Ranked retrieval model;
Use SMART notation: lnc.ltc;
在Dictionary和posting list中存储每个term的DF；
## 实验过程
### 1.在实验一的基础上，添加一些数据结构来储存tf和df：
``` javascript
postings = defaultdict(dict)
document_frequency = defaultdict(int)
```
### 2.修改get_postings函数使之遍历tweets统计并记录tf：
``` javascript
def get_postings_dl():
    global postings, document_lengths
    f = open(
        r"C:\Users\Lenovo\Desktop\tweets.txt")
    lines = f.readlines()  # 读取全部内容

    for line in lines:
        line = tokenize_tweet(line)
        tweetid = line[0]  # 这里记录一下tweetid，就弹出
        line.pop(0)
        document_lengths[tweetid] = len(line)  # 这一步直接记录词数
        unique_terms = set(line)
        for te in unique_terms:
            postings[te][tweetid] = line.count(te)
    # 按字典序对postings进行升序排序,但返回的是列表，失去了键值的信息
    # postings = sorted(postings.items(),key = lambda asd:asd[0],reverse=False)
    mylog = open(r"C:\Users\Lenovo\Desktop\Invertedtf.txt", mode='a', encoding='utf-8')

    print(postings,file=mylog)
```
遍历后输出tf文件Invertedtf（部分代码，全部可在Invertedtf.txt中查看）：
``` javascript
defaultdict(<class 'dict'>, {'may': {'28965792812892160': 1, '29254971430014976': 1, '29281084667596800': 1, '29287792064339968': 1, '29362083367751681': 1, '29371237864050689': 1, '29484939808350208': 1, '29607942009389056': 1, '29635195187499009': 1, '29648841024208896': 1, '29716088212168705': 1, '29812340153131008': 1, '29876347409010688': 1, '29880470950912000': 1, '29959012724244480': 1, '29961115022655489': 1, '30219282595979264': 1, '30370913199333376': 1, '30423259409289216': 1, '30526954549547008': 1, '30570299074289664': 1, '30649612721197056': 1, '30719835499397120': 1, '30811692007034880': 1, '30837239881670656': 1, '30897152850919424': 1, '31055301985697792': 1, '31099423782084608': 1, '31139661069942785': 1, '31144800455495681': 1, '31227454337056768': 1, '31289241761746944': 1, '31467720469905408': 1, '31956136651395072': 1, '31969110816464896': 1, '31969296829652992': 1, '31999423072444416': 1, '32061794818195457': 1, '32067497486196736': 1, '32116131632250880': 1, '32126443693547520': 1, '32207793826045952': 1, '32226525818396673': 1, '32229101687279616': 1, '32276842450784256': 1, '32330718071750656': 1, '32461016214278144': 1, '32462481175613440': 1, '32463160648671232': 1, '32485887937875968': 1, '32521637987360768': 1, '32533397763006464': 1, '32542852458221568': 1, '32615879359332354': 1, '32622381050626048': 1, '32811143571443713': 1, '32880949976891392': 1, '32911447176515584': 1, '33230318035009537': 1, '33305131869011969': 1, '33347103187017728': 1, '33356246027345920': 1, '33356335970000896': 1, '33356503989616640': 1, '33483791594946560': 1, '33901964072853504': 1, '34385815979302912': 1, '34396060751241216': 1, '34422424405540864': 1, '34537169615855616': 1, '34619735081488384': 1, '34629289987149824': 1, '34634409118269440': 1, '34658614710898690': 1, '34872339610996737': 1, '34952094221860864': 1, '34952093886320640': 1, '34961985808375808': 1, '34980421284401153': 1, '35124912364457984': 1, '297152140055543810': 1, '297215868297961472': 1, '297244301497339904': 1, '297393111179603969': 1, '297400920973639680': 1, '297442335527149568': 1, '297515756818673666': 1, '297532202718228482': 1, '297565111223205890': 2, '297691712061595648': 1, '298249852322721795': 1, '298250829570396162': 1, '298253572645191680': 1, '298254403125780480': 1, '298255325885247488': 1, '298263110496710656': 1, '298431037850148866': 1, '298547257819684864': 1, '298663083512041472': 1, '298687905419902976': 1, '298756629069975553': 1, '298796558869229568': 1, '298804066677563392': 1, '298804297351716866': 1, '298840548712775680': 1, '298849566478987264': 1, '298853307798151169': 1, '298869992718479361': 1, '299353432408596480': 1, '299353440793001986': 1, '299354564891660289': 1, '299355055625211905': 1, '299358289404256256': 1, '299374416498921472': 1, '299495761933135872': 1, '299659415286583296': 1, '299941238956765184': 1, '300007823536947200': 1, '300195904512724992': 1, '300837037408415744': 1, '300851176440750080': 1, '300943119770324992': 1, '301000543961227264': 1, '301039773303312384': 1, '301143259357540353': 1, '301175626822475777': 1, '301180546745237505': 1, '301249920525029377': 1, '301286486463090688': 1, '301310448509276162': 1, '301344489505710080': 1, '301346032984412161': 1, '301365272248479747': 1, '301397304181673985': 1, '301400399561240576': 2, '301451511362379776': 1, '301451712659603456': 1, '301722618585821184': 1, '301832127673159681': 2, '301832131867471872': 1, '301977296716320768': 1, ……
```
### 3.遍历tweet并统计记录每个单词的df：
```javascript
def initialize_document_frequencies():
    global document_frequency, postings
    for term in postings:
        document_frequency[term] = len(postings[term])
    mylog2 = open(r"C:\Users\Lenovo\Desktop\Inverteddf.txt", mode='a', encoding='utf-8')
    print(document_frequency,file=mylog2)
```
输出Inverteddf（部分代码，完整可见Inverteddf.txt）：
```javascript
defaultdict(<class 'int'>, {'may': 331, 'http': 22567, 'arizona-style': 5, 'rand': 12, 'arus': 10, 'rick': 41, 'rep': 54, 'house': 282, 'to': 7713, 'the': 10014, 'immigration': 79, 'be': 6218, 'say': 1307, 'people': 8, 'kill': 392, 'unlikely': 12, 'pas': 44, 'bill': 320, 'mariah': 6, 'tinyurl.com/4jrjcdz': 1, 'optimist': 3, 'servando': 2, 'shriver': 9, 'pio': 1, 'sargent': 5, 'charity': 27, 'alway': 78, 'mourner': 4, 'recall': 93, 'r': 168, 'ap': 388, 'bit.ly/gqmcdg': 1, 'wa': 979, "'": 3933, 'n': 403, 'sarge': 3, 'an': 810, 'idealism': 3, 'improve': 26, 'skill': 15, 'fantastic': 34, 'technique': 20, 'eversoll': 1, 'ymy': 571, 'bas': 37, 'heide': 1, '2': 495, 'tip': 131, 'fish': 496, 'cast': 60, 'ailsa': 2, 'for': 4373, 'applying-for-financial-aid': 1, 'hang': 28, 'of': 5617, 'financial-aid-essay': 1, 'get': 1240, 'aid': 104, 'proper': 8, 'education': 148, 'financial': 71, 'method': 13, 'ping.fm/bk0r3': 1, 'ok': 71, 'supreme': 85, 'background': 4, 'court': 307, 'brothy': 1, 'nasa': 84, 'check': 183, 'bit.ly/h2jgy9': 1, 'intrusive': 1, 'music': 96, 'rich': 43, 'time': 726, 'mcdonald': 430, 'low': 26, 'all': 656, 'firework': 7, 'hide': 25, 'burgh': 3, "'d": 54, 'not': 1021, 'hansard': 1, 'when': 318, 'alyce': 2, 'youtu.be/bf14xbbcvzg': 1, 'very': 169, 'cont': 19, 'sgt': 2, 'funeral': 57, 'in': 5900, 'quiet': 5, '2day': 9, 'if': 437, 'sweet': 47, 'polish': 6, 'at': 2404, 'and': 4179, 'bono': 4, 'murder': 46, 'i': 2346, 'tabak': 10, 'with': 2049, 'jo': 23, 'hi': 568, 'yeate': 17, 'polouse': 192, 'have': 1223, 'otherwise': 5, 'vincent': 22, 'really': 704, 'gareth': 3, "'re": 190, 'avon': 1, 'so': 591, 'charge': 127, 'hope': 134, 'they': 563, 'right': 250, 'ruin': 22, 'life': 214, 'somerset': 2, 'patriot': 14, 't.co/1uxya0r': 1, 'sr': 12, 'gov': 34, 'vium': 1707, 'obama\\u2019': 20, 'hawaius': 41, 'update': 247, 'addthi': 51, 'birth': 44, 'eric': 62, 'u2013': 389, 'certificate': 22, 'w': 185, 'waffle': 2, 'belko': 1, 'on': 4205, 'ive': 5, 'myself': 27, 'mcgregor': 1, 'retweeted': 2, 'rt': 3692, 'bit.ly/i0kden': 1, 'my': 1049, 'want': 315, 'tommy': 11, 'atu2': 1, 'but': 638, 'never': 131, 'tommymcgregor': 1, 'sing': 45, 'litt': 1, 'world': 945, 'news': 2820, 'bit.ly/id1qio': 1, 'oprah': 32, 'secret': 128, 'will': 1160, 'wait': 390, 'divulge': 1, 'family': 194, 'her': 254, 'o': 140, 'big': 280, 'chai': 1, 'weekly': 31, 'nuclear': 1126, 'align': 4, 'bit.ly/e78urg': 1, 'talk': 286, 'washington': 201, 'end': 193, 'u': 1536, 'official': 237, 'agreement': 243, 'six': 40, 'blog': 193, 'post': 319, 'power': 205, 'no': 690, 'fox': 217, 'iran': 1392, 'martell': 4, 'focu': 25, 'more': 763, 'unemployment': 76, 'over': 781, 'figure': 31, 'nine': 19, 'bit.ly/el4klf': 1, 'loss': 5, 'job': 159, 'percent': 56, 'thornton': 8, 't': 217, 'obama': 512, 'seemingly': 1, 'steady': 3, 'glenn': 66, 'manufacturer': 8, 'network': 115, 'automat': 1, 'cyber': 70, 'controller': 1, 'turn': 91, 'any': 141, 'elli': 12, 'worm': 3, 'bit.ly/gybgew': 1, 'computer': 53, 'industrial': 13, 'kind': 41, 'bar': 24, 'sundance': 77, '2011': 195,……
```
### 4.查询实现
查询relevant_tweetids：
利用已有数据结构实现查询的功能，对于输入的一串语句，进行相同的token处理，而后为了加快检索速率，避免去遍历所有tweet计算每一个F（q,d）,可以先对于查询检索提取出相关的tweetid,得到relevant_tweetids列表，然后对相关tweetid计算score，降序输出topk个相关tweets。
```javascript
  unique_query = set(query)
  relevant_tweetids = Union([set(postings[term].keys()) for term in unique_query])
```
计算score:
然后对query中的每一个键值对（term，id），计算score:
```javascripit
    for term in unique_query:
        wtq=query.count(term)/len(query)

        if (term in postings) and (id in postings[term].keys()):
            wtd = (1 + math.log(postings[term][id]) * math.log((document_numbers + 1) / document_frequency[term]))
            similarity = wtq*wtd
```
排序：
调用sorted函数对score进行排序:
```javascript
        scores = sorted([(id, Getscore(query, id) 
                          for id in relevant_tweetids],
                         key=lambda x: x[1],
                         reverse=True)
```
输出:
输出前k个值:
```javascript
        for (id, score) in scores3:
            if i<=10:
                result.append(id)
                print(str(score) + ": " + id)
                i = i + 1
            else:
                break
        print("finished")
```
最后调用不同的计算方法来计算相关性

## 
