# limit

```
package limit // import "github.com/mjolnir42/limit"

Package limit implements a concurrency limit.

type Limit struct{ ... }
    func NewLimit(parallel uint32) *Limit

func NewLimit(parallel uint32) *Limit
    NewLimit returns a new concurrency limit

type Limit struct {
	// Has unexported fields.
}
    Limit can be used to limit concurrency on a resource to a specific number of
    goroutines, for example the number of active in-flight HTTP requests.

    l := limit.NewLimit(4)
    ...
    go func() {
        l.Start()
        defer l.Done()
        ... use resource ...
    }()

    Not calling Done() will over time starve l and render the limit permanently
    reached, blocking all Start() requests.


func NewLimit(parallel uint32) *Limit
func (l *Limit) Done()
func (l *Limit) Start()
```
