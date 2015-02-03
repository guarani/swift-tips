# swift-tips

Create an instance of a class from a string.
```
    // Note: This is what a mangled class name looks like _TtC15Test_Reflection17PVSViewController
    // It has a format: See http://www.eswick.com/2014/06/inside-swift/
    let className = "PVSViewController"
    let appName = NSBundle.mainBundle().objectForInfoDictionaryKey("CFBundleName") as String
    let appNameNoSpaces = appName.stringByReplacingOccurrencesOfString(" ", withString: "_", options: .LiteralSearch, range: nil)
    let mangledClassName = "_TtC\(countElements(appNameNoSpaces))\(appNameNoSpaces)\(countElements(className))\(className)"
    var anyobjectype : AnyObject.Type = NSClassFromString(mangledClassName)
    var nsobjectype : NSObject.Type = anyobjectype as NSObject.Type
    var rec: UIViewController = nsobjectype() as UIViewController
    println(rec.view)
```
Instantiate an object from a mangled type name.
``` 
    var anyobjectype : AnyObject.Type = NSClassFromString("_TtC15Test_Reflection17PVSViewController")
    var nsobjectype : NSObject.Type = anyobjectype as NSObject.Type
    var rec: UIViewController = nsobjectype() as UIViewController
```
Introspect an object at runtime using Xcode Version 6.1.1 (6A2008a).
````
    var a = PVSViewController()
        
    println("\(_stdlib_getTypeName(a))")            // _TtC15Test_Reflection17PVSViewController
    println("\(_stdlib_getDemangledTypeName(a))")   // Test_Reflection.PVSViewController
    println("\(a.dynamicType))")                    // (Metatype))
    println("\(a.dynamicType.description())")       // Test_Reflection.PVSViewController
        
    println("\(object_getClassName(a))")            // 0x00007fd35a74fcd0
    println("\(reflect(a).summary)")                // Test_Reflection.PVSViewController
    println("\(a.description)")                     // <Test_Reflection.PVSViewController: 0x7fd35a74b9d0>
```

