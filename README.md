# intransigentms-quests

## Quest *.toml files for the IntransigentMS Maplestory private server

This repository holds all of the quest data for custom quests in IntransigentMS. The format is [TOML (Tom's Obvious Minimal Language)](https://github.com/toml-lang/toml), parsed by the server using [toml4j](https://github.com/mwanji/toml4j) (MIT License).

Here is an example of a quest data file for a dummy quest that showcases all the possible places for information to go:

```toml
# Custom quest, ID: 1234567

title = "This Isn't Even A Real Quest"
npc = "Alice The NPC [Àplace]"
endnpc = "Bob The NPC [À Nötherplace]"
info = """
If you're in-game and you're reading this, something is terribly wrong.

This isn't even a real quest; it's incredibly unimaginative and is clearly a forced example.

That being said, if you still want to do this quest, you can click the #rAccept#k button below..."""

repeatable = true


[requirements]
quests = [1234565, 1234566]
# Checking that the player's level is at least as large
# as their buddy list, which is, as we all know,
# the usual criterion for allowing a player to start a quest.
predicates = [
    """
    function(p) {
        var buddyCap = p.getBuddyList().getCapacity();
        return p.getLevel() >= buddyCap;
    }
    """
]


[[items]]
id = 1302031
name = "Diao Chan Sword"
count = 2

[[items]]
id = 4000418
name = "Useless Mechanical Heart"
count = 666


[[monsters]]
id = 2230107
name = "Krappy"
count = 1

[[monsters]]
id = 9420539
name = "Vikerola"
count = 18

[[monsters]]
id = 130101
name = "Red Snail"
count = 111


[[objectives]]
name = "Do some jumping jacks"
count = 20


[par]
fearless = 54
valiant = 77
adventuresome = 91


[rewards]
exp = 11111111
mesos = 222222
    [[rewards.items]]
    id = 1902006
    count = 1

    [[rewards.items]]
    id = 3991051
    count = 6
consumers = [
    """
    var AbstractPlayerInteraction =
        Java.type(
            "net.sf.odinms.scripting.AbstractPlayerInteraction"
        );

    var rewards =
    [
        3991029, 4031455, 1472062, 4031750,
        1452002, 1322014
    ];

    function(p) {
        var api = new AbstractPlayerInteraction(p.getClient());
        var randReward = rewards[Math.floor(Math.random() * rewards.length)];

        api.gainItem(randReward, 2, true, true);
    }
    """
]

```
