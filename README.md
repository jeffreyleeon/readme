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

#### Predefine actions in fairyActions.json

fairyActions.json stores array of jsons defining Action objects</br>

Required params:
```
id(unique), duration, action_type, (Addtional params based on action_type)
```

There are 9 action_type available (Addtional params follow):
* "MoveTo" - x, y
* "MoveBy" - x, y
* "RotateTo" - degree
* "RotateBy" - degree
* "ScaleTo" - x, y
* "ScaleBy" - x, y
* "FadeTo" - opacity
* "FadeIn"
* "FadeOut"

Example,
```
[
    {
        "id": 1,
        "duration": 2.0,
        "action_type": "MoveTo",
        "x": 100.0,
        "y": 200.0
    },
    {
        "id": 2,
        "duration": 2.0,
        "action_type": "MoveBy",
        "x": 100.0,
        "y": 200.0
    },
    {
        "id": 3,
        "duration": 2.0,
        "action_type": "RotateTo",
        "degree": 90.0
    },
    {
        "id": 4,
        "duration": 2.0,
        "action_type": "RotateBy",
        "degree": 90.0
    },
    {
        "id": 5,
        "duration": 2.0,
        "action_type": "ScaleTo",
        "x": 2.0,
        "y": 2.0
    },
    {
        "id": 6,
        "duration": 2.0,
        "action_type": "ScaleBy",
        "x": 2.0,
        "y": 2.0
    },
    {
        "id": 7,
        "duration": 2.0,
        "action_type": "FadeTo",
        "opacity": 255.0
    },
    {
        "id": 8,
        "duration": 2.0,
        "action_type": "FadeIn"
    },
    {
        "id": 9,
        "duration": 2.0,
        "action_type": "FadeOut"
    }
]

```
