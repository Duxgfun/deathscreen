# DeathScreen – Confiq Team

Plugin thay thế death screen mặc định của Minecraft bằng một death screen của dòng game soul.


## Tổng quan hoạt động

Khi người chơi **đáng lẽ chết** (nhận sát thương chí mạng):

- Plugin **chặn cái chết thật**
- Chuyển người chơi sang **Spectator**
- Đặt camera nhìn vào vị trí chết
- Khoá góc nhìn (không xoay lung tung)
- Hiện title/subtitle
- Sau một khoảng thời gian:
  - Teleport về spawn
  - Hồi **đầy máu + thức ăn**
  - Khôi phục gamemode

Toàn bộ quá trình **không bao giờ kích hoạt death screen mặc định**.

---

## Tính năng chính

### 1. Death cinematic (camera)
- Camera được đặt tại vị trí offset so với điểm chết
- Có thể tuỳ chỉnh offset X/Y/Z
- Camera **luôn nhìn vào điểm chết**

### 2. Title / Subtitle
- Hiển thị title, sub-title text
- Có fade in / stay / fade out
- Hỗ trợ placeholder

### 3. Khoá hành vi
Tuỳ chọn chặn trong cinematic:
- Di chuyển
- Xoay camera
- Tương tác
- Dùng command
- Mở inventory


## Giải thích config.yml

### `deathscreen.enabled`
```yml
enabled: true
````

Bật / tắt toàn bộ plugin.

---

### `deathscreen.trigger`

```yml
trigger:
  interceptLethalDamage: true
  debounceTicks: 20
```

* `interceptLethalDamage`
  Bắt sát thương chí mạng (`finalDamage >= health`)

* `debounceTicks`
  Chống kích hoạt lặp nhiều lần trong thời gian ngắn
  (tránh loop chết)

---

### `deathscreen.cinematic`

#### Spectator

```yml
spectatorMode: true
```

Trong cinematic, người chơi sẽ ở **Gamemode Spectator**.

---

#### Camera offset

Vị trí camera so với điểm chết:

```yml
cameraOffset:
  dx: 3.0
  dy: 4.0
  dz: 0.0
```

#### Nhìn vào điểm chết

```yml
lookAt:
  enabled: true
  targetYOffset: 1.0
```

* `enabled`: bật ép hướng nhìn
* `targetYOffset`: nhìn cao hơn chân (thân/ngực)

#### Delay title

```yml
titleDelayTicks: 0
```

Delay trước khi hiện title (ticks).

#### Khoá hành vi

```yml
lock:
  movement: true
  rotation: true
  interact: true
  commands: true
  inventory: true
```

* `movement`: chặn di chuyển
* `rotation`: **khoá pitch + yaw**
* `interact`: chặn click
* `commands`: chặn command
* `inventory`: chặn inventory

### `deathscreen.ui`

```yml
ui:
  title: "&cYOU DIED"
  subtitle: "&7<message>"
  fadeInTicks: 10
  stayTicks: 40
  fadeOutTicks: 10
```

* Text hiển thị trên màn hình
* Hỗ trợ mã màu `&`
* Timing giống title vanilla

### `deathscreen.return`

```yml
return:
  mode: "PLAYER_SPAWN"
  delayTicks: 60
```

* `mode`:

  * `PLAYER_SPAWN`: giường / respawn anchor
  * `WORLD_SPAWN`: spawn world
  * `CUSTOM`: toạ độ cố định

* `delayTicks`: thời gian cinematic

#### Custom spawn

```yml
custom:
  world: "world"
  x: 0.5
  y: 64.0
  z: 0.5
  yaw: 0.0
  pitch: 0.0
```

### `deathscreen.gamemodeAfter`

```yml
gamemodeAfter:
  mode: "RESTORE_PREVIOUS"
```

* `RESTORE_PREVIOUS`: trả về gamemode cũ
* `FORCE_SURVIVAL`: ép Survival

### `deathscreen.placeholders`

```yml
placeholders:
  enabled: true
```

Placeholder hỗ trợ:

| Placeholder | Ý nghĩa               |
| ----------- | --------------------- |
| `<player>`  | Tên người chơi        |
| `<message>` | Nguyên nhân chết      |
| `<killer>`  | Entity gây sát thương |
| `<cause>`   | DamageCause           |
