[![PyPI version](https://badge.fury.io/py/pycalil.svg)](https://badge.fury.io/py/pycalil)
# pycalil
カーリル図書館APIをpythonから使えるようにしたパッケージ

※事前に[APIキーの取得](https://calil.jp/api/dashboard/)をお願いします
## Requirement
- requests

## installation
```
pip install pycalil
```

## Usage
```python
from pycalil import Pycalil

apikey = "your apikey"
calil = Pycalil(apikey)

# library：https://api.calil.jp/library -----------------------------
# 指定した条件で図書館の一覧を取得する

# pref：都道府県で指定する
# city：市区町村で指定する　※prefとセットで使う。
print(calil.library(pref="青森県", city="青森市"))

"""
json([{"category": "SMALL", "city": "青森市", "short": "中央市民センター", "libkey": "中央市民センター", "pref": "青森県", "primary": false, "faid": null, "geocode": "140.7608082,40.8206974", "systemid": "Aomori_Aomori", "address": "青森県青森市松原1丁目6番15号", "libid": "100251", "tel": "017-734-0163", "systemname": "青森県青森市", "isil": null, "post": "030-0813", "url_pc": "http://www.city.aomori.aomori.jp/chuo-center/kodomo-kyouiku/shimin-center/kouminkan/06.html", "formal": "青森市中央市民センター図書室"},...
"""

# systemid：図書館のシステムIDで指定する
print(calil.library(systemid="Aomori_Pref"))

"""
json([{"category": "LARGE", "city": "青森市", "short": "青森県立図書館　", "libkey": "青県図", "pref": "青森県", "primary": true, "faid": "FA012896", "geocode": "140.7385051,40.7952048", "systemid": "Aomori_Pref", "address": "青森県青森市荒川藤戸119-7 ", "libid": "100287", "tel": "017-739-4211", "systemname": "青森県立図書館", "isil": "JP-1000175", "post": "030-0184", "url_pc": "http://www.plib.pref.aomori.lg.jp/top/index.html", "formal": "青森県立図書館　"}]);
"""

# geocode：緯度、経度で指定する
print(calil.library(geocode="136.7163027,35.390516"))

"""
json([{"category": "SPECIAL", "city": "岐阜市", "short": "岐阜県総合教育センター", "libkey": "本館", "distance": 0.00025125403859339114, "pref": "岐阜県", "primary": true, "faid": null, "geocode": "136.7163027,35.3905132", "systemid": "Gifu_Education_Center", "address": "岐阜県岐阜市薮田南5丁目9-1 岐阜県総合教育センター本館3階", "libid": "100853", "tel": "058-271-3404", "systemname": "岐阜県総合教育センター", "isil": "JP-1005642", "post": "500-8384", "url_pc": "http://www.gifu-net.ed.jp/ssd/tosyo/index.html", "formal": "岐阜県総合教育センター図書・教育資料室"},
"""

# limit：取得するデータの件数を指定
print(calil.library(pref="青森県", city="青森市", limit=2))

"""
json([{"category": "SMALL", "city": "青森市", "short": "中央市民センター", "libkey": "中央市民センター", "pref": "青森県", "primary": false, "faid": null, "geocode": "140.7608082,40.8206974", "systemid": "Aomori_Aomori", "address": "青森県青森市松原1丁目6番15号", "libid": "100251", "tel": "017-734-0163", "systemname": "青森県青森市", "isil": null, "post": "030-0813", "url_pc": "http://www.city.aomori.aomori.jp/chuo-center/kodomo-kyouiku/shimin-center/kouminkan/06.html", "formal": "青森市中央市民センター図書室"}, {"category": "SMALL", "city": "青森市", "short": "北部市民センター", "libkey": "北部市民センター", "pref": "青森県", "primary": false, "faid": null, "geocode": "140.6759542,40.8862817", "systemid": "Aomori_Aomori", "address": "青森県青森市奥内字宮田41番地3", "libid": "100252", "tel": "017-754-2244", "systemname": "青森県青森市", "isil": null, "post": "038-0054", "url_pc": "http://www.city.aomori.aomori.jp/chuo-center/kodomo-kyouiku/shimin-center/kouminkan/02.html", "formal": "青森市北部地区農村環境改善センター（北部市民センター）図書室"}]);
None
"""

# check：https://api.calil.jp/check　　-----------------------------
# 図書館に対して蔵書の有無と貸出状況を問い合わせる 

# isbn：第一引数。書籍のISBNを指定する
# systemid：第二引数。システムIDを指定します
print(calil.check([4003400313], ["Tokyo_NDL"]))

"""
json({"session": "2461f8923302e3dfd5e2a52bec9dad57", "continue": 0, "books": {"4003400313": {"Tokyo_NDL": {"status": "OK", "libkey": {"東京本館": "蔵書あり"}, "reserveurl": "https://ndlonline.ndl.go.jp/#!/detail/R300000001-I000002695283-00"}}}});
"""

```

## Note
APIに関して引数や戻り値などの詳しい仕様
- https://calil.jp/doc/api_ref.html

## Author
- warada0209
- email：[warada0209@gmail.com](warada0209@gmail.com)

## License
"pycalil" is under MIT license.
