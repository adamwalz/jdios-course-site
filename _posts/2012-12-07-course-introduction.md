---
layout: post
title: Course Introduction Spring 2013
excerpt: First lecture of this new course, iOS Programming. This lecture will cover course logistics, determine the level of the students, and explain the course emphasis project as well as how we will utilize github for programming assignments.
category: lectures
tags:
- logistics
- project
- github
- tools
---

<iframe class="youtube-player" type="text/html" width="560" height="315" src="http://www.youtube.com/embed/diP-o_JxysA" frameborder="0" allowfullscreen>
</iframe>

```objectivec
#import <UIKit/UIKit.h>
#import "Dependency.h"

@protocol WorldDataSource
@optional
- (NSString*)worldName;
@required
- (BOOL)allowsToLive;
@end

@interface Test : NSObject <HelloDelegate, WorldDataSource> {
  NSString *_greeting;
}

@property (nonatomic, readonly) NSString *greeting;
- (IBAction) show;
@end

@implementation Test

@synthesize test=_test;

+ (id) test {
  return [self testWithGreeting:@"Hello, world!\nFoo bar!"];
}

+ (id) testWithGreeting:(NSString*)greeting {
  return [[[self alloc] initWithGreeting:greeting] autorelease];
}

- (id) initWithGreeting:(NSString*)greeting {
  if ( (self = [super init]) ) {
    _greeting = [greeting retain];
  }
  return self;
}

- (void) dealloc {
  [_greeting release];
  [super dealloc];
}

@end
```