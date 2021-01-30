# goimports 微调版

## 现状
goimports会对连续的import行进行排序，即仅对每个`段落`内的import行进行排序。所以常常会产生如下的效果：（请自行挑刺^_^）
```go
import (
	"net/url"

	"context"
	"time"
	
	"strconv"
	"testing"

	"reflect"

	"github.com/agiledragon/gomonkey"
	"github.com/smartystreets/goconvey/convey"
)
```
我们常常需要**手动**删去import行之间的换行，以达到我们想要的格式。

## 微调之后

微调了`sortimports.go`的源代码后，goimports会所有import行进行排序，上面的代码**自动**会被排成这样：
```go
import(
	"context"
	"net/url"
	"reflect"
	"strconv"
	"testing"
	"time"

	"github.com/agiledragon/gomonkey"
	"github.com/smartystreets/goconvey/convey"
)
```

### 意义

`开发者`不必每次commit之前检查import格式了，省时间更省心力。

`评审人`也自然不用盯着imports格式，可以专心于检查逻辑。

### 使用方法

```bash
# 下载代码略过

# 进入goimports文件夹
cd cmd/goimports

# 编译出goimports
go build goimports.go

# 查看现有goimports路径
where goimports
# 假设得到了/xx/yy/zz的路径

# 可以替换原goimports
cp goimports /xx/yy/zz/goimports

# 也可以复制新goimports到原goimports路径，以防不时之需要用到原版goimports
cp goimports /xx/yy/zz/goimports_lusong
```

如果没替换goimports，需要手动修改触发goimports的IDE的配置。

以goland为例：
在你的`goland->Preferences->Tools->File Watchers->goimports`下把
`Program`参数从`goimports`改为`goimports_lusong`
