# NavMesh

## 坑

### Agent必须挂在实体上

如果Agent不挂在实体上(如挂在空物体上), 无法触发.

### 用了Nav Mesh不需要再用 Character Controller

Nav Mesh带了碰撞, 即角色会自动下降到接触地面后再开始行动, 如果再挂载Controller就很多余,而且会影响方向调整