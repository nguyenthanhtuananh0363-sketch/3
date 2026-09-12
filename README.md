<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Sokoban Game</title>
  <style>
    body { font-family: monospace; background: #222; color: #fff; text-align: center; margin-top: 50px; }
    #board { display: inline-block; white-space: pre; background: #000; padding: 15px; border-radius: 8px; font-size: 20px; line-height: 1.2; text-align: left; }
    .info { margin-top: 15px; color: #aaa; }
  </style>
</head>
<body>
  <h1>Sokoban Game</h1>
  <div id="board"></div>
  <div class="info">Dùng phím mũi tên <b>⬆️ ⬇️ ⬅️ ➡️</b> để di chuyển</div>

  <script>
    const map = [
      "###########",
      "#### ######",
      "###  ###  #",
      "## $      #",
      "#   @$ #  #",
      "### $###   #",
      "###   #.. #",
      "###  ##.# #",
      "##      ##",
      "##     ####",
      "###########"
    ];

    let grid = map.map(row => row.split(''));
    let playerPos = { r: 4, c: 4 };

    function render() {
      document.getElementById('board').textContent = grid.map(row => row.join('')).join('\n');
    }

    window.addEventListener('keydown', (e) => {
      let dr = 0, dc = 0;
      if (e.key === 'ArrowUp') dr = -1;
      else if (e.key === 'ArrowDown') dr = 1;
      else if (e.key === 'ArrowLeft') dc = -1;
      else if (e.key === 'ArrowRight') dc = 1;
      else return;

      let nr = playerPos.r + dr;
      let nc = playerPos.c + dc;

      if (grid[nr][nc] === ' ' || grid[nr][nc] === '.') {
        grid[playerPos.r][playerPos.c] = map[playerPos.r][playerPos.c] === '.' ? '.' : ' ';
        playerPos = { r: nr, c: nc };
        grid[nr][nc] = '@';
      } else if (grid[nr][nc] === '$') {
        let nnr = nr + dr, nnc = nc + dc;
        if (grid[nnr][nnc] === ' ' || grid[nnr][nnc] === '.') {
          grid[nnr][nnc] = '$';
          grid[playerPos.r][playerPos.c] = map[playerPos.r][playerPos.c] === '.' ? '.' : ' ';
          playerPos = { r: nr, c: nc };
          grid[nr][nc] = '@';
        }
      }
      render();
    });

    render();
  </script>
</body>
</html>
