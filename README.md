## Fairy System

1. Include Fairy Layer

Add Fairy Layer to the top most of the scene that will use the fairy system

```
#include "FairyLayer.h"

fairyLayer = FairyLayer::create();
addChild(fairyLayer, 1000);
```

2. Call Fairy Guide with FairyTrigger object

FairyTrigger takes 4 parameters

* Vec2 position - 2D vector position of fairy on screen
* std::string words - Sentence that fairy will say
* float duration - Time fairy will stay on screen, if duration <= 0.0, fairy will be remove when user tap the screen
* Action* action - Animation that fairy will perform

```
Vec2 position = Vec2(100.0, 200.0);
std::string words = "Example Sentence";
float duration = 5.0;
Action* action = MoveTo::create(duration, Vec(0, 0));
FairyTrigger* trigger = new FairyTrigger(position, words, duration, action);
fairyLayer->runTrigger(trigger);
```
