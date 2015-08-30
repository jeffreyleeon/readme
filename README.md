## Fairy System

#### Include Fairy Layer

Add Fairy Layer to the top most of the scene that will use the fairy system

```
#include "FairyLayer.h"

fairyLayer = FairyLayer::create();
addChild(fairyLayer, 1000);
```

#### Call Fairy Guide with FairyTrigger object

FairyLayer takes a FairyTrigger object to display fairy <br/>
FairyTrigger takes 4 parameters

* Vec2 position - 2D vector position of fairy on screen
* std::string words - Sentence that fairy will say
* float duration - Time fairy will stay on screen, if duration <= 0.0, fairy will be remove when user tap the screen
* Action* action - Animation that fairy will perform, if no action required, set nullptr

```
Vec2 position = Vec2(100.0, 200.0);
std::string words = "Example Sentence";
float duration = 5.0;
Action* action = MoveTo::create(duration, Vec(0, 0));
FairyTrigger* trigger = new FairyTrigger(position, words, duration, action);
/* Trigger without action
FairyTrigger* trigger = new FairyTrigger(position, words, duration, nullptr);
*/
fairyLayer->runTrigger(trigger);
```

#### Predefine triggers in fairyTriggers.json

fairyTriggers.json stores array of jsons defining fairyTrigger objects
```
[
    {
        "id": 1,
        "x": 0.0,
        "y": 0.0,
        "words": "First sentence",
        "duration": 0.0,
        "actions": [1, 2],
        "is_sequential": true,
        "is_repeating": false
    },
    {
        "id": 2,
        "x": 900.0,
        "y": 150.0,
        "words": "Second sentence",
        "duration": 5.0
    }
]
```

Required params:
```
id(unique), x, y, words, duration
```
Optional params:
```
actions, is_sequential, is_repeating
```
(Optional params are all required if `actions` is needed)

In the below case,<br/>
fairyTrigger with id 1 will display a fairy in position (0, 0) saying "First sentence".<br/>
fairyTrigger with id 2 will display a fairy in position (900.0, 150.0) saying "Second sentence", stays 5.0 seconds.
```
fairyLayer->runTriggerWithId(1);
fairyLayer->runTriggerWithId(2);
```

#### Call triggers with key

triggersKeyIdPair.json stores json with key, trigger id pairs.<br/>
User can run trigger with key. (Beaware that trigger id must appear in fairyTriggers.json)
```
{
    "SettingScreen::onEnter": 1,
    "PenIntroduction::onEnter": 2
}
```
In SettingScreen.m
```
void SettingsScreen::onEnter() {
    Layer::onEnter();
    fairyLayer->runTriggerWithKey("SettingScreen::onEnter");
}
```
fairyTrigger with id 1 will be displayed in the above case
