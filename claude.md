## Leaflet.js 地図描画の注意事項

### placeLabels と fitBounds の順序

`placeLabels()` 内の `map.latLngToContainerPoint()` は
**現在の地図ビュー（中心・ズーム）に依存する**。

`fitBounds` で地図が動く前に `placeLabels` を呼ぶと
座標変換がずれてラベルや線の位置がおかしくなる。

**正しい順序：**
```javascript
map.once('moveend', () => placeLabels());
map.fitBounds(bounds, {padding:[60,60], animate:false});
