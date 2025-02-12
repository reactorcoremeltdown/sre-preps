# **30 Golang Questions for SRE/DevOps Interviews (With Answers)**  

Golang is widely used in **systems administration, automation, and cloud tooling** due to its efficiency, concurrency support, and ease of deployment. Below are **30 commonly asked** Golang interview questions with detailed answers, focusing on **SRE/DevOps** use cases.  

---

## **1. Why is Golang popular for SRE/DevOps tasks?**  
Golang is **fast, statically compiled**, has **built-in concurrency**, and **cross-compilation support**, making it ideal for **CLI tools, system utilities, and cloud-native applications**.  

---

## **2. How do you execute a shell command in Golang?**  
Use `os/exec`:  
```go
package main

import (
	"fmt"
	"os/exec"
)

func main() {
	out, err := exec.Command("ls", "-l").Output()
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	fmt.Println(string(out))
}
```
---

## **3. How do you read environment variables in Go?**  
Use `os.Getenv`:  
```go
package main

import (
	"fmt"
	"os"
)

func main() {
	fmt.Println("HOME:", os.Getenv("HOME"))
}
```
---

## **4. How do you create and write to a file in Go?**  
Use `os.Create` and `WriteString`:  
```go
package main

import (
	"os"
)

func main() {
	file, _ := os.Create("test.txt")
	defer file.Close()
	file.WriteString("Hello, World!")
}
```
---

## **5. How do you handle errors in Go?**  
Use `if err != nil`:  
```go
if err != nil {
	fmt.Println("Error:", err)
	return
}
```
---

## **6. What are Goroutines and why are they useful in DevOps tools?**  
**Goroutines** are lightweight threads managed by Go, allowing concurrent execution without system threads overhead.  
```go
go func() {
	fmt.Println("This runs in a Goroutine")
}()
```
Useful for **log processing, parallel API calls, and monitoring tasks**.

---

## **7. How do you limit Goroutines to prevent excessive resource usage?**  
Use a **worker pool with buffered channels**:  
```go
package main

import (
	"fmt"
	"time"
)

func worker(id int, jobs <-chan int) {
	for job := range jobs {
		fmt.Printf("Worker %d processing job %d\n", id, job)
		time.Sleep(time.Second)
	}
}

func main() {
	jobs := make(chan int, 5)
	for i := 1; i <= 3; i++ {
		go worker(i, jobs)
	}
	for j := 1; j <= 10; j++ {
		jobs <- j
	}
	close(jobs)
}
```
---

## **8. How do you parse JSON in Golang?**  
Use `encoding/json`:  
```go
package main

import (
	"encoding/json"
	"fmt"
)

type Data struct {
	Name string `json:"name"`
}

func main() {
	jsonStr := `{"name": "DevOps"}`
	var d Data
	json.Unmarshal([]byte(jsonStr), &d)
	fmt.Println(d.Name)
}
```
---

## **9. How do you make an HTTP GET request in Go?**  
Use `net/http`:  
```go
resp, _ := http.Get("https://example.com")
defer resp.Body.Close()
```
---

## **10. How do you build a simple HTTP server?**  
```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "Hello, World!")
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServe(":8080", nil)
}
```
---

## **11. How do you run background tasks in Golang?**  
Use `go func() {}`:  
```go
go func() {
	time.Sleep(time.Second * 5)
	fmt.Println("Task done")
}()
```
---

## **12. How do you write logs in Go?**  
Use the `log` package:  
```go
log.Println("This is a log message")
```
---

## **13. How do you handle timeouts in Go?**  
Use `context.WithTimeout`:  
```go
ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
defer cancel()
```
---

## **14. How do you compile Go code for different platforms?**  
```sh
GOOS=linux GOARCH=amd64 go build -o mytool-linux
```
---

## **15. How do you create a CLI tool in Go?**  
Use `github.com/spf13/cobra` or `flag` package:  
```go
package main

import (
	"flag"
	"fmt"
)

func main() {
	name := flag.String("name", "DevOps", "User name")
	flag.Parse()
	fmt.Println("Hello,", *name)
}
```
Run with:  
```sh
go run main.go -name=SRE
```
---

## **16. How do you generate random numbers in Go?**  
```go
rand.Seed(time.Now().UnixNano())
fmt.Println(rand.Intn(100))
```
---

## **17. How do you create a TCP server in Golang?**  
Use `net` package:  
```go
ln, _ := net.Listen("tcp", ":8080")
```
---

## **18. How do you monitor system resource usage in Go?**  
Use `github.com/shirou/gopsutil`:  
```go
import "github.com/shirou/gopsutil/cpu"
cpu.Percent(0, true)
```
---

## **19. How do you interact with Docker from Go?**  
Use the **Docker API** via `github.com/docker/docker/client`:  
```go
cli, _ := client.NewClientWithOpts(client.FromEnv)
cli.ContainerList(context.Background(), types.ContainerListOptions{})
```
---

## **20. How do you parse command-line arguments?**  
Use `os.Args`:  
```go
fmt.Println(os.Args[1:])
```
---

## **21. How do you set a timeout for an HTTP request?**  
```go
client := &http.Client{Timeout: 5 * time.Second}
```
---

## **22. How do you validate JSON input in Go?**  
Use `json.Unmarshal` with struct validation.  
---

## **23. How do you use mutexes in Golang?**  
Use `sync.Mutex`:  
```go
var mu sync.Mutex
mu.Lock()
mu.Unlock()
```
---

## **24. How do you store persistent configuration in Go?**  
Use `viper`:  
```go
viper.SetConfigName("config")
viper.ReadInConfig()
```
---

## **25. How do you handle signals (like Ctrl+C)?**  
```go
import "os/signal"
```
---

## **26. How do you create a worker queue?**  
Use `goroutines` and `channels`.  
---

## **27. How do you unit test a function in Golang?**  
Use `testing` package:  
```go
func TestSomething(t *testing.T) {
	t.Errorf("Failed test")
}
```
---

## **28. How do you format Go code?**  
Use `gofmt`:  
```sh
gofmt -w myfile.go
```
---

## **29. How do you build a simple Prometheus exporter in Go?**  
Use `github.com/prometheus/client_golang/prometheus`.  
---

## **30. How do you run a Go binary inside a minimal Docker container?**  
```Dockerfile
FROM alpine:latest
COPY mybinary /usr/bin/
CMD ["/usr/bin/mybinary"]
```
---

## **Final Thoughts**  
These **30 Golang questions** will help you **prepare for SRE/DevOps interviews**! 🚀