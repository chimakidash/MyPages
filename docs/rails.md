
# rails syntax 

## ローカル変数(var)
小文字またはアンダーバー(_)で始まる変数は「ローカル変数」と呼ばれます。ブロック内、メソッド内などローカルなスコープで有効です。

```ruby
Ruby
def func()
  var = 123
end
```

## インスタンス変数(@var)
アットマーク(@) で始まる変数は「インスタンス変数」と呼ばれます。そのオブジェクトが存在する間有効です。インスタンス変数は、自クラスやサブクラスから参照できます。

```ruby
Ruby
class MyClass
  def setName(str)
    @name = str
  end

  def getName()
    return @name
  end
end

obj1 = MyClass.new()
obj2 = MyClass.new()
obj1.setName("Tanaka")
puts obj1.getName()           # => Tanaka
puts obj2.getName()           # => nil
```

---

## DNSサーバ起動時に発生するエラー

### journalctl -u named

```
dns_rdata_fromtext: hoge.zone:x: near eol: unexpected end of input
```

想定される問題: ゾーンファイル「hoge.zone」のx行目に不正な改行や空白が存在する際に発生する。

> SOAレコードに改行が存在している(SOAレコードは改行不可)
> hoge.zone の先頭行がTTLではない
> 先頭行が空白で始まる


```
hoge.zone:x: SOA record not at top of zone (hogehoge.zone.hogehoge.zone)
```

想定される問題: ゾーンファイル「hoge.zone」のSOAレコードのroot domain指定が漏れている

> hoge.zone のSOAレコードにおいて、「hogehoge.zone.」 の最終.(ドット)が抜けている

```
dns_rdata_fromtext: hoge.zone:x: near 'hogehoge.zone.': not a valid number
```

想定される問題: ゾーンファイル「hoge.zone」のx行目に存在するレコードの書式が正しくない

> MXレコードの優先度を書き忘れた

