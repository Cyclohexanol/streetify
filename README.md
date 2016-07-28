#Introduction

Streetify is a 2D godlike simulation game. It is based on an alien planet where the inhabitants have an underdeveloped civilization. The goal is to macro-manage this civilization in order to prosper as much as possible.

## Player interaction

The player plays the role of a "god". He can not give orders to any inhabitants or build things himself, however he can affect the overall behavior of the civilization by controlling macro elements such as government type, climate, civilization goals, available research etc.

As civilization evolves and makes discoveries. The player can decide what the focus of the research will be and what the government focus should be (education, healthcare, war, etc.)

## The world

The concept is that the world is perceived in 2 dimensions - height and width. One "map" forms a street. As the player advances though the game, more streets will be added forming a city and later on cities. The user can move from one street to another using a map menu. The playable map is always rendered as a street.

The street is a simple 2D array with square tiles. It has different layers to test object collision.

### Layers

#### Layer 0: landscape

The background landscape. It is mainly decorative and can not be altered. It can however show the seasons, time of the day or even climate.

#### Layer 1: building

The building wall layer. When a building is built. This layer tests that there is no collision with another one. The back walls are drawn on this layer.

#### layer 2: items

The item layer. This is where items are places and their collision is tested - see items section for more details.

#### Layer 3: units

The unit layer.


### Units

The world is populated by aliens who form civilization. Each unit has an AI and take decision bases upon many factors (personal needs, personal interest, personal capacity, government goals, money, beliefs...). The population grow as the game progresses through immigration or breeding.

Units have individual traits and a simplified DNA meaning through breeding and as the generations go on, the population can mutate and develop new traits or lose some. The base traits of the primitive units and the immigrants are randomly generated.

### Land and buildings

Units can own land where they can build buildings. The size of the land and the buildings are decided by the unit's AI. Units can then add items to their buildings. Buildings have rooms and each room has a purposes for example "bedroom" to sleep. Units can buy or create items - see items section below - and add them to the rooms they own. This can affect some properties of the room. For example adding a shelf to a shop increases the storage capacity whereas adding a plant increases the attractiveness of the establishment.

Buildings do not store a "type" however rooms do. Thus, a unit can own a small building with only a small apartment for himself and then decide to build a new room to it to start his shop or his factory. As the game develops, more types are added such as restaurants, labs or government buildings.
