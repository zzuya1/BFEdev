# issue #
As the opposite of Partial<T>, Required<T> sets all properties of T to required.
Please implement MyRequired<T> by yourself.
```
// all properties are optional
type Foo = {
  a?: string
  b?: number
  c?: boolean
}
const a: MyRequired<Foo> = {}
// Error
const b: MyRequired<Foo> = {
  a: 'BFE.dev'
}
// Error
const c: MyRequired<Foo> = {
  b: 123
}
// Error
const d: MyRequired<Foo> = {
  b: 123,
  c: true
}
// Error
const e: MyRequired<Foo> = {
  a: 'BFE.dev',
  b: 123,
  c: true
}
// valid
```
# answer #
```
type MyRequired<T> = {[P in keyof T]-?:T[P];}
```
# analysis #
+ `P in keyof T` will iterate over the all properties of type T
+ `-?` will remove the optionality of attributes
+ `T[P]` represents getting the property that is P in type T
