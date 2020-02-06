# Turtle-eat-fish-20200207-
A game designed to allow turtle eating fish
import random as r

class Turtle(object):
    
    def __init__(self):
        self.power = 100              # 设置初始生命值100
        self.x = r.randint(0,10)      # 设置乌龟的初始位置，随机
        self.y = r.randint(0,10)      # 函数详见下方截图
        
    def move(self):
        new_x = r.choice([1,2,-1,-2]) + self.x   # 移动后的新x轴坐标 = 移动步长 + 初始位置
        new_y = r.choice([1,2,-1,-2]) + self.y
                                                 # 然后判断移动后的位置有否出界，并进行出界后调整
                                                 # 先对x轴进行判断调整
        if new_x < 0:
            self.x = 0 - (new_x - 0)
        elif new_x > 10:
            self.x = 10 - (new_x - 10)
        else:
            self.x = new_x
                                                 # 再对y轴进行判断调整
        if new_y < 0:
            self.y = 0 - (new_y - 0)
        elif new_y > 10:
            self.y = 10 - (new_y - 10)
        else:
            self.y = new_y
                                                 # 为了移动，消耗相应的体力值
        self.power -= 1
        return (self.x, self.y)                  # 这里周老师用的是return
    
    def eat(self):                               # 乌龟吃鱼可以增加体力
        self.power += 20
        if self.power >= 100:
            self.power = 100                     # 体力值的上限就是100

            
class Fish(object):
    def __init__(self):
        self.x = r.randint(0,10)
        self.y = r.randint(0,10)
                                                 # 第一步，定义鱼的初始坐标，x方向上，and y方向上，随机初始坐标

    def move(self):
        new_x = r.choice([1,-1]) + self.x
        new_y = r.choice([1,-1]) + self.y
                                                 # 第二步，定义如何移动以及移动后的位置, x和 y方向上。 
                                                 # 并且对移动后的位置要进行判断，是否出界。正式位置更新。
        if new_x < 0:
            self.x = 0 + (0 - new_x)
        elif new_x > 10:
            self.x = 10 - (new_x - 10)
        else:
            self.x = new_x
        
        if new_y < 0:
            self.y = 0 + (0 - new_y)
        elif new_y > 10:
            self.y = 10 - (new_y - 10)
        else:
            self.y = new_y
                                                 # 最后，要返回鱼的最终位置，正式 位置更新
        return (self.x, self.y)
    

turtle = Turtle()                                # 实例化一只乌龟
fish = []                                        # 鱼池 初始是一个空列表
for i in range(10):                              # 设置鱼池的最大值，最多是10条鱼， 从 0到 9
    new_fish = Fish()                            # 每一条新投入鱼池的鱼，都属于 鱼 这个类
    fish.append(new_fish)                        # 每投放完一条，要计数

while True:
    if not len(fish):
        print("All fish eaten up. GAME OVER!")
        break
    if not turtle.power:
        print("Turtle is out of power. GAME OVER!")
        break
    
    pos = turtle.move()                          # 将每一次turtle移动后的坐标位置，返回给 pos
    
    for each_fish in fish[:]:                    # 用for循环，因为最多只有 10 条鱼
        if each_fish.move() == pos:              # 每当鱼移动到了乌龟的位置上，两个等号，判断是否位置相合
            turtle.eat()                         # 执行乌龟吃鱼 这个 动作/函数
            fish.remove(each_fish)               # 这个remove要非常当心
            print("Eat a fish~")
