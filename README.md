# go-genGinRouter

按 https://github.com/swaggo/gin-swagger 编写注释,然后自动生成路由

编写 go 文件并添加注释
```go
package xxx
// @BasePath /api/v1

// HelloWorld PingExample godoc
// @Summary ping example
// @Schemes
// @Description do ping
// @Tags example
// @Accept json
// @Produce json
// @Success 200 {string} HelloWorld
// @Router /example/helloworld [delete]
func HelloWorld(g *gin.Context) {
    g.String(http.StatusOK, "helloworld")
}
type Test struct {
    Name string `json:"name" query:"name" validate:"min=5"`
}
// HelloWorld1 PingExample godoc
// @Summary ping example
// @Schemes
// @Description do ping
// @Tags example
// @Accept json
// @Produce json
// @Success 200 {string} HelloWorld
// @Router /example/helloworld1 [get]
func (t Test) HelloWorld1(g *gin.Context) {
    g.String(http.StatusOK, t.Name)
}
```

```go
//go:generate go install github.com/mzzsfy/go-genGinRouter@latest
//go:generate go-genGinRouter

var g = gin.Default()

func init() {
    routers.RegisterErrorHandle(g)
    routers.RegisterRouter(func() *gin.Engine { return g })
}
func main() {
    g.Run(":8080")
}
```

```
go generate
```

已知问题 @BasePath 不被 gin-swagger 正确解析

本项目支持每个文件一个@BasePath,不支持全局@BasePath
