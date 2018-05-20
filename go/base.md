#### `defer`

该语句用于延迟调用制定的函数,它只能出现在函数的内部,尤`defer`关键字及函数组成

* 当外围函数的代码引起恐慌的时候,只有其中所有的延迟函数都执行完毕后,该运行时恐慌才会真正被扩散至调用函数
* 当执行外围函数中的return语句的时候,只有其中所有的延迟函数都执行完毕后,外围的函数才会真正返回



###### 执行顺序

Defer & Return执行顺序如下:

```Go
func main() {
	fmt.Println(a())    //0
}
func a() int {
	var i int
	defer func() {
		i++
		fmt.Println("defer1:", i)    //defer1:2
	}()
	defer func() {
		i++
		fmt.Println("defer2:", i)   //defer2:1
	}()
	return i
}

```



有名返回值

```Go
func main() {
	fmt.Println(b()) //2
}

func b() (i int) {
	defer func() {
		i++
		fmt.Println("defer1:", i) //defer1:2
	}()
	defer func() {
		i++
		fmt.Println("defer2:", i) //defer2:1
	}()
	return i
}
```



看了上面两个例子,我们可以得出结论

* defer执行顺序是后进先出
* Defer,return,返回值三者,return 最先执行,其次是defer,最后将返回值带回

```
func main(){
    fmt.Println(*c()) //2
}

func c() *int {
	var i int

	defer func() {
		i++
		fmt.Println("defer1:", i)

	}()
	defer func() {
		i++
		fmt.Println("defer2:", i)
	}()
	return &i
}
```



#### recover&panic

```go
defer func(){
    if e:=recovery();e!=nil{
        if se,ok:=e.(scanError);ok{
            err = se.err
        }else{
            panic(e)
        }
    }
}
```

