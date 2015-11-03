# PlaygroundATSBypass
Bypass Apple's new App Transport Security inside a playground to use Charles when experimenting with an API.


```swift
// When using Charles, the network requests will always fail unless you can bypass ATS.
class NetworkEnabler: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(.UseCredential, NSURLCredential(trust: challenge.protectionSpace.serverTrust!))
    }
}
let enabler = NetworkEnabler()
```

This is equivalent to using something like 

```bash
curl --proxy localhost:8888 --insecure -H "Authorization: Bearer c79e539cd1eb46e" https://api.github.com/user
```
