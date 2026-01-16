# Player (Character) Dimensions & Positioning

## Character Sprite (`#character`)

**CSS Location**: `index.html` baris ~207-217

### Ukuran:
- **Width**: 140px
- **Height**: 180px

### Posisi Dasar:
- **Bottom**: 60px (jarak dari bawah viewport)
- **Left**: 50% (centered)
- **Transform**: translateX(-50%) (untuk center horizontal)
- **Position**: fixed (tetap di viewport)

### Jump Animation (`charJump`):
- **Bottom range**: 60px → 170px → 60px
- **Duration**: 0.6s
- **Easing**: cubic-bezier(0.34, 1.56, 0.64, 1)
- **Scale Y**: Berubah dari 1 → 0.7 → 1 (compression effect)

## Ground Collision Detection

**JavaScript Location**: `index.html` baris ~890-900 (dalam function `updatePlayer`)

### Ground Position:
```javascript
const groundY = window.innerHeight - 240;
```

Ini berarti player akan menyentuh tanah pada **240px dari bawah layar**.

### Jump Settings:
- **Jump Force**: -15 (velocity)
- **Gravity**: 0.6 (acceleration per frame)
- **Is Jumping**: Tracked dengan `gameState.isJumping`

## Gates (Collision Areas)

### Next Gate (`.gate`):
- **Position**: bottom 25%, right 5%
- **Collision**: Menggunakan `getBoundingClientRect()`
- **Trigger**: Menyentuh gate → `levelComplete()` → go to next level

### Previous Gate (`.gate-prev`):
- **Position**: bottom 25%, left 5%
- **Collision**: Menggunakan `getBoundingClientRect()`
- **Trigger**: Menyentuh gate → `levelCompletePrev()` → go to previous level

## Mengubah Ukuran Player

Jika ingin mengubah ukuran player:
1. Edit CSS width & height di `#character { width: X; height: Y; }`
2. Edit `gameState.playerWidth` dan `gameState.playerHeight` di JavaScript
3. Sesuaikan `bottom: 60px;` untuk posisi vertikal dasar
4. Update `charJump` animation values jika perlu

## Mengubah Ground Level

Jika ingin mengubah tinggi ground:
1. Edit `const groundY = window.innerHeight - 240;` di function `updatePlayer()`
2. Nilai 240 adalah jarak dari bawah (HUD ada di bottom: 0, tinggi 60px, jadi space di atas adalah 240px)
