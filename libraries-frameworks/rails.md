# Rails

## Rspec
* `let` - lazily evaluate a block, the object is not created until it is needed
* `let!` - forcefully evaluated, the object is available as soon as its defined
* `let_it_be` - forcefully create variables once before all tests are run, similar to defining in a `before_all`

### Tips
* Spring is an application preloader, which will keep your application running in the background after boot
* run `rspec` tests with spring to avoid booting your application for every test run 
