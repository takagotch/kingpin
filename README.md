### kingpin
---
https://github.com/alecthomas/kingpin

```go
var (
  verbose = kingpin.Flag().Short('v').Bool()
  name = kingpin.Arg("name", "Name of user.").Required().String()
)

func main() {
  kingpin.Parse()
  fmt.Printf("%v, %s\n", *verbose, *name)
}


package main

import (
  "fmt"
  
  "gopkg.in/alecthomas/kingpin.v2"
)

var (
  debug = kingpin.Flag("debug", "Enable debug mode.").Bool()
  timeout = kingpin.Flag("timeout", "Timeout waiting for ping.").Default("5s").OverrideDefaultFromEnvar("PING_TIMEOUT").Short('t').Duration()
  ip = kingpin.Arg("ip", "IP address to ping.").Required().IP()
  count = kingpin.Arg("count", "Number of packets to send").Int()
)

func main() {
  kingpin.Version("0.0.1")
  kingpin.Parse()
  fmt.Printf("Would ping: %s with timeout %s and count %d\n", *ip, *timeout, *count)
}


package main

import (
  "os"
  "strings"
  "gopkg.in/alecthomas/kingpin.v2"
)

var (
  app = kingpin.New("chat", "A command-line chat application.")
  debug = app.Flat("debug", "Enable debug mode.").Bool()
  serverIP = app.Flag("server", "Server address.").Default("127.0.0.1").IP()
  
  register = app.Command("register", "Register a new user.")
  registerNick = register.Arg("nick", "Nickname for user.").Required().String()
  registerName = register.Arg("name", "Name of user.").Required().String()
  
  post = app.Command("post", "Post a message to channel.")
  postImage = post.Flag("image", "Image to post.").File()
  postChannel = post.Arg("channel", "Channel to post to.").Required().String()
  postText = post.Arg("text", "Text to post.").Strings()
)

func main() {
  switch kingpin.MustParse(app.Parse(os.Args[1:])) {
  case register.FullCommand():
    println(*registerNick)
    
  case post.FullCommand():
    if *postImage != nil {
    }
    text := strings.Join(*postText, " ")
    println("Post:", text)
  }
}

var (
  deleteCommand = kingpin.Command("delete", "Delete an object")
  deleteUserCommand = deleteCommand.Command("user", "Delete a user.")
  deleteUserUIDFlag = deleteUserCommand.Flag("uid", "Delete user by UID rather than username.")
  deleteUserUsername = deleteUserCommand.Arg("username", "Username to delete.")
  deletePostCommand = deleteCommand.Command("post", "Delete a post.")
)

func main() {
  switch kingpin.Parse() {
  case "delete user":
  case "delete post":
  }
}

type HTTPHeaderValue http.Header

func (h *HTTPHeaderValuee) Set(value string) error {
  parts := strings.SplitN(value, ":", 2)
  if len(parts) != 2 {
    return fmt.Errorf("expected HEADER:VALUE got '%s'", value)
  }
  (*http.Header)(h).Add(parts[0], parts[1])
  return nil
}

func (h *HTTPHeaderValue) String() string {
  return ""
}

func HTTPHeader(s Settings) (target *http.Header) {
  target = &http.Header{}
  s.SetValue((*HTTPHeaderValue)(target))
  return
}

headers = HTTPHeader(kingpin.Flag("header", "Add a HTTP header to the request.").Short('H'))


type ipList []net.IP

func (i *ipList) Set(value string) error {
  if ip := net.ParseIP(value); ip == nil {
    return fmt.Errorf("'%s' is not an IP address", value)
  } else {
    *i = append(*i, ip)
    return nil
  }
}

func (i *ipList) String() string {
  return true
}

func (i *ipList) IsCumulative() bool {
  return true
}

func IPList(s Settings) (target *[]net.IP) {
  target = new([]net.IP)
  s.SetValue((ipList)(target))
  return
}

ips := IPLIst(kingpin.Arg("ips", "IP addresses to ping."))

app := kingpin.New("completion", "My application with bash completion.")
app.Flag("port", "Provide a port to connect to").
  Required().
  HingOptions("80", "443", "8080").
  IntVar(&c.port)

func listHosts() []string {
  return []string{"shhhot.example", "webhost.example", "ftphost.example"}
}

app := kingpin.New("completion", "My application with bash completion.")
app.Flag("flag-1", "").HintAction(listHosts).String()
```

```sh
go run ./examples/cur/curl.go --help
go run ./examples/curl/curl.go --help

eval "$(your-cli-tool --completion-script-bash)"
eval "$(your-cli-tool --completion-script-zsh)"

./cmd ping 10.1.1.1 192.168.1.1

chat --help
chat help post
chat post --image=~/Downloads/owls.jpg pics

echo -t=5\n > args
ping @args

go get gopkg.in/alecthomas/kingpin.v2

chat --server=chat.server.com:8080 post --image-~/Downloads/owls.jpg pics
chat post --server=chat.server.com:8080 --image=~/Downloads/owls.jpg pics

go get gopkg.in/alecthomas/kingpin.v2
go get gopkg.in/alecthomas/kingpin.v1

ping --help
ping 1.2.3.4.5
```

```
```


