```typescript
  class Promise<T> {
    state: string;
    value: T
    resolveFns = []
    rejectFns = []
    constructor (fn) {
      this.state = 'pending'
      fn(this.resolve, this.reject)
    }
    private resolve (data) {
      this.state = 'fulfilled'
      this.value = data;
      this.resolveFns.forEach((fn)=>{
        this.value = fn(this.value)
      })
    }
    private reject (data) {
      this.state = 'rejected';
      this.catch(data)
    }
    public then(resolveFn, rejectFn) {
      this.resolveFns.push(resolveFn)
      this.rejectFns.push(rejectFn)
      return new Promise()
    }
    public catch() {

    }
  }

```