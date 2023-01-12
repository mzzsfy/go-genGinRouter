# go-genGinRouter

配合 https://github.com/swaggo/swag 

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
