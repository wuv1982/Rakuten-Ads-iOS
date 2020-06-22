[TOP](/README.md#top)　>　 Banner Ads

---

# Banner Ads

RUNABanner SDK banner view is a web view bases on `WebKit/WKWebView` which will present advertisement content by loading HTML advertisement tags.

---

## 1. Configurations

### 1.1 AdSpotID

`Ad Spot` is considerred as a placement where the advertisement is showing.`adSpotId` is the identifier of the `Ad Spot` and is required before requesting a banner ads. It can be found or registerred as a new one on the publisher management webside.

### 1.2 Size

Then banner view has 3 options for designated **size** to support variaty of using cases.
- `default` :<br>
Default option. The banner view's **size** can not be changed programmatically and is depended on the configuration in the `adspotId` registration on the publisher management webside.
- `aspectFit` : <br>
The banner view keeps aspect radio and stretches its width to fit the super view's width.
- `custom` :<br>
The banner view can be indicated to arbitrary size and ignores the orginal size.


### 1.3 Position

The banner view's **position** can be set in anywhere of the screen in demand. The SDK also has six preset position settings with the auto layout features to give some convienence during the integration.

### 1.4 Event Tracker

The RUNABanner SDK tracks 3 event types of `RUNABannerViewEvent` if developers need to be triggerred and handle something by themselves.

- **Succeeded (RUNABannerViewEventTypeSucceeded) :**<br>
  Succeeded to received the advertisement response.

- **Failed (RUNABannerViewEventTypeFailed) :**<br>
  Failed to send, receive or show the advertisement. 
  
  Detail of the failure with error information can be found in RUNABannerViewError property and the system console logs. 
  - `none` : No error.
  - `internal` : Unexpected internal error of SDK.
  - `network` : Network issues.
  - `fatal` : Mistake settings.
  - `unfilled` : Request received while there is no advertisement sources to show.

- **Clicked (RUNABannerViewEventTypeClicked) :**<br>
  After the banner is clicked.


## 2. Samples

![Language](http://img.shields.io/badge/language-ObjctiveC-red.svg?style=flat)

```objc
#import <RUNABanner/RUNABanner.h>

RUNABannerView* banner = [RUNABannerView new];

banner.adSpotId = @"spot_id_xxx";
banner.position = RUNABannerViewPositionBottom;

[banner loadWithEventHandler:^(RUNABannerView * _Nonnull view, struct RUNABannerViewEvent event) {
    switch (event.eventType) {
        case RUNABannerViewEventTypeSucceeded:
            NSLog(@"received event succeeded");
            [banner setCenter:[self.view center]];
            break;
        case RUNABannerViewEventTypeFailed:
            NSLog(@"received event failed");
            switch (event.error) {
                case RUNABannerViewErrorUnfilled:
                    NSLog(@"ad unfilled");
                    break;
                case RUNABannerViewErrorNetwork:
                    NSLog(@"network unavailable");
                    break;
                default:
                    break;
            }
            break;
        case RUNABannerViewEventTypeClicked:
            NSLog(@"received event clicked");
            break;
        default:
            NSLog(@"unknown event");
            break;
    }
}];
[self.view addSubview:banner];
```

![Language](http://img.shields.io/badge/language-Swift-red.svg?style=flat)

```swift
import RUNABanner

let banner = RUNABannerView()

banner.adSpotId = "adspot_id_xxx"
banner.position = .bottom

banner.load { (banner, event) in
    switch event.eventType {
    case .succeeded:
        print("received event succceeded")
    case .failed:
        print("received event failed")
        switch event.error {
        case .unfilled:
            print("ad available")
        case .network:
            print("network available")
        default:
            break
        }
    case .clicked:
        print("received event clicked")
    default:
        break
    }
}

self.view.addSubview(banner)
```

---

[TOP](/README.md#top)

---

LANGUAGE :

> [![ja](/doc/lang/ja.png)](/doc/ja/bannerads/README.md)