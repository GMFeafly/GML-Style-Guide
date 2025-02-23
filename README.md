# Naming
Good naming conventions are essential for writing clean, maintainable, and collaborative code.

## 1. **Variables**
- **Local Variables**: Use `snake_case` with descriptive names  
  ```gml
  var bullet_speed = 5;
  var player_score = 0;
  ```

- **Instance Variables**: Prefix with `_` for private-like variables  
  ```gml
  _health = 100;       // Internal state
  attack_cooldown = 0; // Public/modifiable variable
  ```

- **Global Variables**: Use explicit `global.` scope  
  
  ```gml
  global.game_difficulty = 2;  // Avoid ambiguous names like "global.diff"
  ```

## 2. **Constants**
- Use `ALL_CAPS` with meaningful groupings:  
  ```gml
  #macro MAX_PLAYERS 4
  #macro TILE_SIZE 32
  #macro COLOR_UI #FF0000
  ```

## 3. **Functions/Methods**
- **General Functions**: `verb_noun()` structure  
  ```gml
  function calculate_damage() { /*...*/ }
  function spawn_enemy() { /*...*/ }
  ```

- **Boolean Functions**: Start with `is_`, `has_`, `can_`  
  ```gml
  function is_grounded() { /*...*/ }
  function has_powerup() { /*...*/ }
  ```

## 4. **Script Names**
- Group logically with prefixes:
  ```gml
  /// @description Physics system
  scr_physics_collision();
  scr_physics_gravity();
  
  /// @description UI system
  scr_ui_dialog();
  scr_ui_inventory();
  ```

## 5. **Objects/Resources**
| Resource Types | Prefixes | Examples      | Short Form Prefixes | Examples   |
| -------------- | -------- | ------------- | ------------------- | ---------- |
| Room           | rm_      | rm_setting    | r                   | rSetting   |
| Object         | obj_     | obj_player    | o                   | oPlayer    |
| Timeline       | tl_      | tl_story      | t                   | tStory     |
| Sequence       | seq_     | seq_shop      | seq                 | seqShop    |
| Font           | fnt_     | fnt_arial     | fn                  | fnArial    |
| Shader         | sha_     | sha_glass     | sh                  | shGlass    |
| Script         | scr_     | scr_name      | f                   | fName      |
| Path           | path_    | path_action   | pth                 | pthAction  |
| Sound          | snd_     | snd_ambience  | sn                  | snAmbience |
| TileSet        | ts_      | ts_forest     | t                   | tForest    |
| Sprite         | spr_     | spr_explosion | s                   | sExplosion |

## 6. **Key Conventions**
1. **Avoid Ambiguity** 
   ❌ `var a = 10;` → ✅ `var enemy_spawn_delay = 10;`

2. **Context Matters** 

   ```gml
   // In player object:
   hp = 100;        // Obvious in player context
   boss_hp = 500;   // Explicit in global scope
   ```

3. **No Magic Numbers**: 
   ❌ `if (speed > 9)` → ✅ `#macro MAX_SPEED 9`

## 7. **Special Cases**
- **Arrays**:
  
  ```gml
  var weapon_list = array_create(0);  // Better than "var wl = []"
  ```
  
- **DS Maps/Lists**:
  
  ```gml
  var achievement_data = ds_map_create();  // Clearer than "var data_map"
  ```

# Comments

## 1. Basic Commenting Principles

### 1.1 Single-Line Comments
```gml
// Use double slashes for brief explanations
hspeed = 5; // Horizontal movement speed
```

### 1.2 Multi-Line Comments
```gml
/* 
 * Use slash-asterisk format for longer explanations
 * Maintain consistent asterisk alignment
 * Explain complex algorithms here
 */
```

## 2. Documentation Comments
```gml
/// @description Creates particle effect at given position
/// @param {number} x X-coordinate for effect
/// @param {number} y Y-coordinate for effect
/// @param {string} type Effect type from particle system
function create_effect(x, y, type) {
    // Implementation...
}
```

## 3. Contextual Guidelines

### 3.1 Functional Headers
```gml
// ----------------------------
// PLAYER STATE MACHINE
// Handles all player transitions:
// - Idle → Run
// - Run → Jump
// - Jump → Fall
// ----------------------------
```

### 3.2 Complex Logic
```gml
// Calculate diagonal movement using Pythagorean theorem
var _move_speed = speed * 0.7071; // 1/√2 approximation
```

## 4. Anti-Patterns to Avoid

❌ Redundant comments:
```gml
x += 1; // Add 1 to x
```

❌ Outdated comments:
```gml
// Old platform detection (removed in v2.3)
// if (place_meeting(x, y, obj_floor))...
```

## 5. Special Comment Tags

```gml
// TODO: Implement double jump mechanics
// FIXME: Collision detection fails at high speeds
// HACK: Temporary workaround for mobile input
```

## 6. Collaborative Notation

```gml
// [DEV NOTE: Feafly - 2025-02-23]
// This pathfinding implementation should be replaced
// with A* algorithm in future updates
```

# Code Formatting

## 1. Line Length
- **Maximum 80 characters per line**
- Break long lines at logical points:
  ```js
  // Good
  draw_sprite_ext(sprite_index, image_index, x, y, image_xscale, 
                   image_yscale, image_angle, image_blend, image_alpha);
  
  // Avoid
  draw_sprite_ext(sprite_index,image_index,x,y,image_xscale,image_yscale,image_angle,image_blend,image_alpha);
  ```

## 2. Indentation
- **Whether using spaces or tabs**, you always need to have an indentation.
  
  ```js
  if (condition) {
    do_something();
  }
  ```

## 3. Anonymous Functions
- Keep concise (≤3 lines)
- Format multi-line functions:
  ```js
  var func_ending = function() {
    instance_destroy();
    audio_play_sound(snd_explode, 10);
  };
  ```

## 4. Function Calls
- Space after commas:
  ```js
  instance_create_layer(x, y, "Characters", obj_player);
  ```

## 5. Control Structures
### 5.1 Conditionals
```js
if (hp <= 0) {
  die();
} else if (hp < 25) {
  play_sound(snd_low_health);
} else {
  // Empty else blocks discouraged
}
```

### 5.2 Loops
```js
for (var i = 0; i < array_length(arr); i++) {
  process_element(arr[i]);
}

while (!place_free(x, y)) {
  y -= 1;
}
```

### 5.3 Switch Statements
```js
switch (keyboard_key) {
  case vk_left:
    x -= speed;
    break;
    
  case vk_right:
    x += speed;
    break;
    
  default:
    // Handle default case
}
```

## 6. Return Statements
- Keep simple returns on one line:
  ```js
  function calculate_damage() {
    return base_damage * multiplier;
  }
  ```

## 7. Variable Initialization
- One declaration per line:
  ```js
  var player_x = x;
  var player_y = y;
  var inventory = [];
  ```

## 8. Preprocessor Directives
- Start at column 1:
  ```js
  #macro MAX_PLAYERS 4
  #region DEBUG_FUNCTIONS
  function show_debug_info() {
    // ...
  }
  #endregion
  ```

## 9. Horizontal Whitespace
- Use around operators:
  ```js
  var result = (a * b) + (c / d);
  ```
- No space inside parentheses:
  ```js
  if (place_meeting(x, y, obj_wall))  // Good
  if ( place_meeting(x, y, obj_wall) ) // Avoid
  ```

## 10. Vertical Whitespace
- **1 blank line** between functions:
  ```js
  function jump() {
    // ...
  }
  
  function attack() {
    // ...
  }
  ```
