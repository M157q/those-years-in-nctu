===================
20150512 Trace Code
===================

最近學長待的公司（A）和另一間公司（B）有合作案，請 B 公司寫了一些程式，前一陣子學長請我開始 Trace Code，因為這份 Code 是用 Python 寫的，學長這邊因為案子的關係沒有人寫過。

B 公司的軟體 License 都賣好幾十萬的，Code 應該 ok 吧。

開起來先瞄了一下，好像沒什麼奇怪的地方。縮排都是四個空白，沒有混用 tab 和空白之類的。範例程式短短的不到 100 行，應該還好。

我對 Trace Code 真的很不拿手，拿這個來練習應該不錯？

文件是 docx，嗯...應該只是習慣。

----

不，我期待太多了，這份一定是初學者寫的。

澄清一下，我覺得這份 Code 一定是 Python 初學者寫的，但他應該有寫過其他語言。他的邏輯沒有問題，就只是對 Python 很不了解。

我一邊 Trace 一邊寫這篇吧。

----

::

  #!/usr/bin/python

如果我用 FreeBSD，Python 放在 ``/usr/local/bin`` 咧？

這份 Code 需要 Python2，如果我的系統預設就是 Python3 呢？

----

::

  import json as json
  import random as random
  import pycurl as pycurl

沒必要把 ``json`` import 進來改名成 ``json`` 啦。

----

::

  elif request_type != "PUT" and request_type != "DELETE" and request_type != "GET":

其實可以用 ``request_type not in ('PUT', 'DELETE', 'GET'):``

----

::

  ...
  print("Type ./run.py --help to know usage.")
  sys.exit()
  ...
  print("Type ./run.py --help to know usage.")
  sys.exit()
  ...

（英文文法就不提了）有種東西叫做函式，用 ``def`` 可以定義出來。

----

::

  ret = []
  for i in range(len(var_list)):
      var_name = var_list[i]
      var_id = int(var_name[2:])
      var_id = "openflow:" + str(var_id)
      ret.append(var_id)
  return ret

（變數名稱已通通更換）

出現了，C 式的 for-loop，Python 裡面的 for 是 for-each 啊，而且不斷的 append，效能會低吧？

``var_id`` 的值先是 ``int`` ，再換成 ``str`` ，最後拿去接 ``str`` ，何苦？

改成這樣會不會好一點？ ::

  return ['openflow:'+ var_name[2:] for var_name for var_list]

----

再來 ::

  flow_flag = "TRUE"
  ...
  if flow_flag == "TRUE":
    ...

Python 有 布 林 值 可 以 用，就是 ``True`` 和 ``False`` ，麻煩先把內建的型別看完再來寫程式好嗎？

----

::

  var_name_b = var_name_a.lower() + "_postfix" + str(j + 1)

格式化字串在 Python2 和 Python3 都有，用一下好嗎不要自己接字串...

----

::

  def func(arg): #comment
      try:
          ...
          return results
      except ValueError as err:
          print(err)

要是 Exception 發生的話，這個函式會回傳 ``None`` ，你真的處理得來嗎？

----

::

  [var_a, var_b] = module.func (param_a, param_b)

為什麼 Function Call 要加一個空白...有些地方有加有些地方還沒加...

----

為什麼要 import 完全沒用到的 module...

----

空白和 tab 混用了啦， **在** **同** **一** **行** **混** **用** **了** **啦** **！**

----

可以不要把 ``filename.py~`` 也包進壓縮檔裡面嗎？

----

這份 Code 是工讀生寫的吧？

心情很複雜。

一套軟體 License 好幾十萬的公司，可以拿這種 Code 出來賣。

初學者就算了， **這他媽的是產品** ，是要賣錢的產品。

我以後會跟這種人共事嗎？我會不會需要 Review 他的 Code？

我會不會被派下任務，幾週後要交出一份 Code，但使用的程式語言我完全沒用過？

我會不會被迫在不習慣的環境下寫程式？

