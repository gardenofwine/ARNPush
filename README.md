# ARNPush

[![CI Status](http://img.shields.io/travis/xxxAIRINxxx/ARNPush.svg?style=flat)](https://travis-ci.org/xxxAIRINxxx/ARNPush)
[![Version](https://img.shields.io/cocoapods/v/ARNPush.svg?style=flat)](http://cocoadocs.org/docsets/ARNPush)
[![License](https://img.shields.io/cocoapods/l/ARNPush.svg?style=flat)](http://cocoadocs.org/docsets/ARNPush)
[![Platform](https://img.shields.io/cocoapods/p/ARNPush.svg?style=flat)](http://cocoadocs.org/docsets/ARNPush)

## Attention

### During the Test....

## Usage

To run the example project, clone the repo, and run `pod install` from the Example directory first.

### AppDelegate

```objective-c

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    [ARNPush setDeviceTokenBlock:^(NSString *deviceToken, NSError *error) {
        if (error) {
            // didFailToRegisterForRemoteNotificationsWithError
        } else {
            // didRegisterForRemoteNotificationsWithDeviceToken
        }
    }];

    [ARNPush setAlertBlock:^(NSDictionary *userInfo) {
        NSLog(@"Call ARNPush Alert Block");
    }];

    [ARNPush setSoundBlock:^(NSDictionary *userInfo) {
        NSLog(@"Call ARNPush Sound Block");
    }];

    [ARNPush setBadgeBlock:^(NSDictionary *userInfo) {
        NSLog(@"Call ARNPush Badge Block");
    }];

    [ARNPush registerForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge)
                launchOptions:launchOptions];

    return YES;
}

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
    // call ARNPush DeviceTokenBlock
}

- (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error
{
    // call ARNPush DeviceTokenBlock
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
{
   // call ARNPush AlertBlock, SoundBlock, BadgeBlock
}

```

## Requirements

* iOS 7.0+
* ARC

## Installation

ARNPush is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

    pod "ARNPush"

## Method Swizzling

replaced the following methods.

```objective-c

- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken;

- (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error;

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo;

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler;

// iOS 8.0+ Only
- (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void(^)())completionHandler;

```

## License

ARNPush is available under the MIT license. See the LICENSE file for more info.

