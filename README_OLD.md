# Introduction

Streetify is a 2D godlike simulation game. It is based on an alien planet where the inhabitants have an underdeveloped civilization. The goal is to macro-manage this civilization in order to prosper as much as possible.

The game offers a canvas with basic content. It is completely opened to modding and encourages the community to create their own content in order to bring the game to the complexity they desire.

## Player interaction

The player plays the role of a "god". He can not give orders to any inhabitants or build things himself, however he can affect the overall behavior of the civilization by controlling macro elements such as government type, climate, civilization goals, available research etc.

As a civilization evolves and makes discoveries. The player can decide what the focus of the research will be and what the government (see government) focus should be (education, healthcare, war, etc.).

The game mode defines how the world is rendered or not (see rendering) and what the player can modify. The game provides a "realtime" game mode with a graphic render of what is happening in real time and console type simulation mode where nothing can be forced by the player after the initial parameters are set. The civilization is then simulate as fast as possible without any render allowing to see an evolution over years within seconds though states and consoled events.

It is possible to imagine many other game mode that can then be added. RPG (can only control one unit nothing else) or even a cookie clicker-style mode where users need to click with their mouse in order to span resources for they civilization.

## Rendering

The game provides a standard render of the entities described below. However, the render and "backend" are totally separated allowing the community to customize the skin of the game.

Separating rendering from the "backend" also allows to skip forwards in time with out losing computational power on graphics. It is possible to imagine playing this game without ever seeing a street, only by view the world in forms of stats and charts, or to leave a world self regulate itself and viewing the result as a timelapse.

## The world

The concept is that the world is perceived in 2 dimensions - height and width. One "map" forms a street. As the player advances though the game, more streets will be added forming a city and later on cities. The user can move from one street to another using a map menu. The playable map is always rendered as a street. Each ends of the street leads to the "wild". Aliens can go to the wild to bring back resources, animals or knowledge to the civilization though hunting, exploring etc... however, the wild is not rendered and does not have a spacial dimension. Aliens are simply tagged as "in the wild".

The street is a simple 2D array with square tiles. It has different layers to test object collision.

### Layers

#### Layer 0: landscape

The background landscape. It is mainly decorative and can not be altered. It can however show the seasons, time of the day or even climate.

#### Layer 1: building

The building wall layer. When a building is built. This layer tests that there is no collision with another one. The back walls are drawn on this layer.

#### Layer 2: wall items

The item layer. This is where wall items are places and their collision is tested - see items section for more details.

#### Layer 3: floor items

The item layer. This is where floor items are places and their collision is tested - see items section for more details.

#### Layer 4: units

The unit layer. Aliens and animals are drawn on this layer. This is the only layer containing entities that does not have a collision constraint.

### Land and buildings

Aliens can own land where they can build buildings. The size of the land and the buildings are decided by the unit's AI. Aliens can then add items to their buildings. Buildings have rooms and each room can have a purposes for example "bedroom" to sleep. Aliens can buy or create items - see items section below - and add them to the rooms they own. This can affect some properties of the room. For example adding a shelf to a shop increases the storage capacity whereas adding a plant increases the attractiveness of the establishment.

Buildings do not store a "type" however rooms do. Thus, an alien can own a small building with only a small apartment for himself and then decide to build a new room to it to start his shop or his factory. As the game develops, more types are added such as restaurants, labs or government buildings. The objects in a room give the room uses and some objects are restricted to a type of room. A "Housing room" can contain a bed which would allow it to be used as a bedroom however a bed can not be placed in a restaurant. Rooms can combine purposes as long as the items can be placed in that rome "type". A "housing room" can be used as a kitchen and a bathroom if it contains a stove and a toilet.

The term "room" is used in a very broad way and it does not require to be part of a closed building. Thus, a yard or a farmland is considered as a "room" even though it does not have solid walls. Some walls be of a special type, such as fence. They are placed on the wall layer, however they do not allow wall items to be placed on them and can not be built on (ie. support a second floor).

### Items

There are three type of items personal, floor and wall. All items can be bought, sold, stored and are crafted by a corresponding type of craftman or later on machines. The craftman's skill or the machine performance determines the quality of that item which affects the effectiveness. Items can get unlocked through research (see research section).

There is no official currency. It works on trading. At the start alien typically just trade an item for another items they want. Later on they might develop a generic currency but that can be anything. One civilization might start using chicken eggs as a currency (causing very obvious issues due to the fact that can rot - these interactions could be very funny as it would force aliens to spend their assets very quickly, this might cause extreme consumerism and everyone building a yard and breeding chickens) or one civilization might go the more standard route by using rare metals. As long as resource is scarce, it can become a currency so this totally depends on the civilization and might change as it develops.

#### Personal items

Personal items can be carried around and used by units. These items can give various modifiers on aliens attributes (see attributes for more information), used for research or simply be used to craft other items. All personal items have a weight. This is a limiting factor to how many items a unit can carry at any given time.

#### Wall and floor items

They are both very similar. They both give bonuses and/or purposes to the room in which they are placed. A painting will give an attractiveness bonus where as bed will give a purpose, sleeping. Some items are restricted to a room "type".

However, they are on different layer allowing them to be combined on the same tile. A painting can be placed behind a shelf as they belong each category respectively. Wall items can only be placed in rooms with walls - see land and buildings section for more information. This means that a farmland can have a scarecrow or a crop plant as it is floor item but cannot have wall lamp.

### Units

#### Aliens

The world is populated by aliens who form a civilization. Each unit has an AI and take decision bases upon many factors (personal needs, personal interest, personal capacity, government goals, money, beliefs...). The population grows as the game progresses through immigration or breeding.

Aliens can have jobs, get married

Aliens have 2 types of traits and list of attributes affecting their behaviors and skills.

Attributes are values that change through the life of an alien - such as thirst, hunger, weight, walking speed, strength, happiness, ...). They can be affected by external factors (an alien will get thirsty faster if the weather hot and dry), personal factors (traits - see traits), activities (an alien will gain happiness if playing games) or by another attribute (having a high weight will decrease walking speed).

Genetic traits and character traits. Genetic traits are defined when the alien is born and will remain the same for the rest of it's life - see genetic traits of examples. These are usually passed on to future generations however can mutate. An alien is also born with character traits, usually similar to his parent. However, character traits can change though out an alien life. Age, society, occupations or drastic events can cause an alien to develop a character trait or loss one - see character traits of examples.

Attributes, skills and genetic traits are stored as numerical values. Character traits are booleans.

#### Animals

Animals can be wild or domesticated. They can come from the wild or breeding.

### The wild

The wild is a dimensionless place where alien can go by reaching the end of the streets. Note that as the street expands the wild can get further away from an house. This could have interesting effects on aliens that depend on the wild, such as hunters.

Resources (animals, food, minerals, discoveries) from the wild can be brought back to the street.

## Technologies

Technology is a simple tree structure. Technology can require prior technologies to be unlocked. Technologies can make new items, jobs, room types, government structure, skills and actions available to the civilization. A technology can be unlock through research or for basic technologies exploration of the wild or the use of a similar objects.

## The government

The government types can vary (dictatorship, communism, democracy...), the government ruler or rulers take decisions affecting the civilization (ie. law on stealing). These decision are based on machine learning. The depth and type of the machine learning used is correlated to the type of government and quality of the ruler. A dumb dictator will take very random decisions using close to no machine learning in them (suddenly wearing cloths might be prohibited in an arctic environment), whereas a very good democratic government with intelligent aliens running it might take very educated and optimized decisions.

## Events

There are two types of events, personal and global.

Personal events can happen anywhere, including the wild, and typically drastically affect one alien (ie. dying, getting paralyzed, finding a stack of gold,...).

Global events affect the entire civilization (ie. earthquakes, plague, ...).

# Ideas

This section contains ideas for content. The goal is to have a canvas that can be modded by other users. The game will be launched with initial content in order to have an enjoyable experience. However, it is up to the community to take the game to the extent of complexity they wish to go.

## Aliens

### Characteristic

#### Attributes

- Age
- Height
- Weight
- Attractiveness
- Boredom
- Energy
- Happiness

#### Skills

- Cooking
- Handyman
- Building
- Cleaning
- Communication
- Trading
- Science
- Math
- Art
- Psychology


#### Genetic traits

- Life expectancy
- Max height
- Corpulence
- Physical aptitude
- Skin color
- Heat tolerance
- Intelligence
- Health

#### Character traits

- Religions
  * Fanatic
  * Atheist
  * Monotheist
  * Polytheist
  * Scientologist
  * ...
- Passion
  * Art
  * Science
  * Animals
  * Nature
  * Food
  * ...
- Phobias
  * Vertigo
  * Arachnophobia
  * People
  * Clostrophobia
  * ...
- Diets
  * Allergies
  * Carnivore
  * Vegetarian
  * Vegan
  * ...
- Disabilities
  * Mute
  * Deaf
  * Paralyzed
- Impatient
- Patient
- Greedy
- Selfish
- Altruist
- Posh
- Good orator
- Natural businessman
- Stubborn
- Influenceable
- Pretentious
- Shy
- Outgoing
- Glutton
- Crazy
- Responsible
- YOLO

### Jobs

- Jobless
- Builder
- Cook
- Hunter
- Writer
- Miner
- Trader
- Businessman
- Handyman
- Farmer
- Doctor

## Rooms types

- Housing
- Lab
- Commerce
- Factory
- Field
- Storage

## Items

### Personal

- Foods
- Metals & rocks
- Plants & seeds
- Woods
-

### Wall & floor

- Bed
- Lamp
- Chairs
