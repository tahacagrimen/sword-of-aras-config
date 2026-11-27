# Sword of Aras — denge ayarları

Oyun açılışta `economy.v1.json` dosyasını okur. `1.0` uygulamanın içindeki dengedir, `1.2` %20 fazla, `0.8` %20 az demektir.

## Nasıl değiştirilir

1. GitHub'da `economy.v1.json` dosyasını aç, kalem simgesine bas, değeri değiştir, **Commit changes**.
2. Yaklaşık 10 dakika içinde yayına girer (GitHub Pages önbelleği).
3. Oyuncu oyunu bir sonraki açışında alır. İnternet yoksa en son aldığı değerlerle oynar.

Geri almak için değeri `1.0` yap. **Dosyayı silme**: silinirse oyuncularda son indirilen değerler kalır.

## Genel + dünya + bölüm

```json
{
  "global": { "enemy_hp": 1.1 },
  "worlds": { "2": { "enemy_damage": 0.9 } },
  "levels": { "17": { "enemy_hp": 0.85 } }
}
```

- Katmanlar çarpılır. Yukarıdaki örnekte 17. bölümde düşman canı `1.1 × 0.85 = 0.935`.
- Dünya numarası 1–5, bölüm numarası 1–120. Her dünyada 24 bölüm var.
- Yazmadığın anahtar `1.0` sayılır.

## Anahtarlar

### Genel, dünya ve bölümde kullanılabilir

| Anahtar | Ne değiştirir |
|---|---|
| `enemy_count` | Dalgalardaki düşman sayısı (boss sayısı değişmez) |
| `enemy_hp` | Düşman canı (boss dahil) |
| `enemy_damage` | Düşman saldırı gücü (boss dahil) |
| `boss_hp` | Sadece boss canı, `enemy_hp` üstüne ek |
| `boss_damage` | Sadece boss saldırı gücü, `enemy_damage` üstüne ek |
| `fort_hp` | Düşman ininin (kulesinin) canı |
| `kill_gold` | Düşman öldürünce gelen altın |
| `clear_gold` | Bölüm bitirme altını ve bonusları |
| `xp` | Öldürmeden gelen tecrübe puanı |
| `drop_chance` | Eşya düşme ihtimali |
| `food_rate` | Yiyecek dolma hızı (saniyede en fazla 12) |
| `mana_rate` | Mana dolma hızı (saniyede en fazla 12) |

### Sadece `global` içinde

| Anahtar | Ne değiştirir |
|---|---|
| `item_bonus` | Eşyaların faydaları (cezaları büyümez) |
| `passive_skill_bonus` | Pasif skillerin seviye başına katkısı (Weapon/Accessory Mastery hariç) |
| `ability_power` | Aktif yeteneklerin gücü (hasar ve iyileştirme) |
| `troop_hp` / `troop_damage` | Asker canı / saldırı gücü |
| `commander_hp` / `commander_damage` | Aras'ın canı / saldırı gücü |
| `upgrade_cost` | Asker yükseltme fiyatı |
| `unlock_cost` | Yeni asker açma fiyatı |
| `shop_price` | Mağaza eşya fiyatı (satış fiyatı da buna uyar) |

## Sınırlar ve dikkat edilecekler

- Değerler `0.1`–`5.0` arasına kırpılır. `enemy_count` için `0.25`–`3.0`.
- Sayılar tırnaksız yazılır (`1.2`, `"1.2"` değil). Tırnaklı değer yok sayılır.
- JSON bozuksa oyun dosyayı yok sayar ve son geçerli değerlerle devam eder.
- Küçük düşman sayılarında yuvarlama yüzünden `1.05` gibi ufak çarpanlar bazı bölümlerde hiçbir şey değiştirmeyebilir.
- Daha çok ya da daha dayanıklı düşman, yıldız sürelerini tutturmayı zorlaştırır.
- `enemy_count` artınca toplam altın, tecrübe ve eşya da artar. İstemiyorsan `kill_gold` ile dengele.
- Savaş sürerken gelen yeni değerler o savaşı etkilemez.
- Uygulama güncellemesiyle temel denge değişirse yeni sürüm `economy.v2.json` okumalı. `v1` eski sürümler için kalır.
