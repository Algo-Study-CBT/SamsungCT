# BOJ 19236 청소년 상어
from sys import stdin
from copy import deepcopy

# arr 배열 초기 입력
def init(arr):
    # stdin = open('input.txt', 'r')
    for x in range(4):
        buf = list(map(int, stdin.readline().split()))
        for y in range(0, len(buf), 2):
            num, dir = buf[y], buf[y + 1]
            arr[x].append([num, dir])

# 방향 전환
def rotate(n):
    return 1 if n == 8 else n + 1

# 물고기가 이동할 수 있는지 체크
def check(x, y, arr):
    if x < 0 or y < 0 or x >= 4 or y >= 4 or arr[x][y] == 'shark':
        return False
    return True

# 물고기 이동
def move(arr):
    global dx, dy
    # 1~16번 물고기 이동
    for i in range(1,17):
        x, y = find(i, arr)
        if x == None:
            continue
        # 이동 가능할 때까지 8번 방향 전환
        for j in range(8):
            dir = arr[x][y][1]
            nx, ny = x + dx[dir], y + dy[dir]
            # 이동할 수 없으면 방향 전환
            if not check(nx, ny, arr):
                arr[x][y][1] = rotate(dir)
                continue
            # 물고기 위치 swap
            tmp = arr[x][y]
            arr[x][y] = arr[nx][ny]
            arr[nx][ny] = tmp
            break

def dfs(next, _arr, _shark):
    global answer, dx, dy
    # 백트래킹을 위해 깊은 복사
    arr, shark = deepcopy(_arr), deepcopy(_shark)

    # 물고기 잡아먹기
    x, y = shark[1]  # 현재 상어의 좌표
    nx, ny = next    # 잡아먹을 물고기 좌표
    fish, dir = arr[nx][ny] # 물고기 정보
    arr[x][y] = None # 현 좌표를 빈칸으로
    arr[nx][ny] = 'shark' # 잡아먹은 위치에 상어 이동
    shark[0] += fish # 잡아먹은 물고기 누적
    shark[1] = (nx, ny) # 잡아먹은 물고기 좌표로 상어 위치 갱신
    shark[2] = dir # 잡아먹은 물고기의 방향으로 변경
    x, y = nx, ny # 좌표 이동
    answer = max(shark[0], answer) # 최대 값 갱신

    move(arr) # 물고기 도망챠!!!

    # 다음 이동 : 최대 3칸 이동 가능
    for i in range(1, 4):
        nx, ny = x + dx[dir]*i, y + dy[dir]*i
        if nx < 0 or ny < 0 or nx >= 4 or ny >= 4 or arr[nx][ny] == None:
            continue
        dfs((nx, ny), arr, shark)


def find(key, arr):
    for x in range(4):
        for y in range(4):
            if arr[x][y] == 'shark' or arr[x][y] == None or key != arr[x][y][0]:
                continue
            return (x, y)
    return (None, None)

# ↑, ↖, ←, ↙, ↓, ↘, →, ↗ 순서
dx = [0, -1, -1, 0, 1, 1, 1, 0, -1]
dy = [0, 0, -1, -1, -1, 0, 1, 1, 1]

answer = 0
shark = [0, (0, 0), 0] # 누적 물고기, 좌표, 방향
arr = [[] for x in range(4)] # 물고기가 들어있는 공간
init(arr)
dfs((0,0), arr, shark)

print(answer)
