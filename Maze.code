from pygame import *

class GamePlayer(sprite.Sprite):
    def __init__(self, p_image, px, py, p_speed, pw, ph):
        self.image = transform.scale(image.load(p_image), (pw, ph))
        self.rect = self.image.get_rect()
        self.rect.x = px
        self.rect.y = py
        self.p_speed = p_speed

    def reset(self):
        wind.blit(self.image, (self.rect.x, self.rect.y))

class Player(GamePlayer):
    def step(self):
        key_pressed = key.get_pressed()
        if key_pressed[K_UP] and self.rect.y > 0:
            self.rect.y -= self.p_speed

        if key_pressed[K_DOWN] and self.rect.y < 421:
            self.rect.y += self.p_speed

        if key_pressed[K_LEFT] and self.rect.x > -9:
            self.rect.x -= self.p_speed

        if key_pressed[K_RIGHT] and self.rect.x < 635:
            self.rect.x += self.p_speed
            
class enemy(GamePlayer):
    direction_s = 'left'
    direction_d = 'down'
    def movement_side(self, x1, x2):
        if self.rect.x <= x1:
            self.direction_s = 'right'
        if self.rect.x >= x2:
            self.direction_s = 'left'
        if self.direction_s == 'left':
            self.rect.x -= self.p_speed
        else:
            self.rect.x += self.p_speed

    def movement_down(self, y1, y2):
        if self.rect.y <= y1:
            self.direction_d = 'up'
        if self.rect.y >= y2:
            self.direction_d = 'down'
        if self.direction_d == 'down':
            self.rect.y -= self.p_speed
        else:
            self.rect.y += self.p_speed

class Walls(sprite.Sprite):
    def __init__(self, color, wall_x, wall_y, wall_w, wall_h):
        super().__init__()
        self.color = color
        self.width = wall_w
        self.height = wall_h
        self.image = Surface((self.width, self.height))
        self.image.fill((color))
        self.rect = self.image.get_rect()
        self.rect.x = wall_x
        self.rect.y = wall_y

    def draw_wall(self):
        wind.blit(self.image, (self.rect.x, self.rect.y))


wind = display.set_mode((700, 500))
background = transform.scale(image.load('bground.webp'), (700, 500))
game = True
FPS = 60
clock = time.Clock()
unlock = False
finish = False
mixer.init()
mixer.music.load('jungles.ogg')
mixer.music.play()
kick = mixer.Sound('kick.ogg')
player = Player('player.png', 0, 200, 5, 40, 40)
spike = enemy('spike.png', 260, 120, 5, 50, 50)
spike2 = enemy('spike.png', 430, 220, 5, 50, 50)
treasure = GamePlayer('treasure.png', 245, 305, 10, 50, 50)
doorkey = Player('key.png', 255, 215, 5, 30, 30)
wall = Walls((0,0,0), 100, 0, 10, 190)
wall2 = Walls((0,0,0), 100, 270, 10, 210)
wall3 = Walls((0,0,0), 320, 0, 10, 290)
wall4 = Walls((0,0,0), 210, 170, 10, 210)
wall5 = Walls((0,0,0), 110, 0, 210, 10)
wall6 = Walls((4,0,0), 110, 470, 600, 10)
wall7 = Walls((0,0,0), 220, 280, 210, 10)
wall8 = Walls((0,0,0), 210, 90, 10, 30)
wall9 = Walls((247,177,0), 320, 290, 10, 80)
wall10 = Walls((0,0,0), 220, 370, 350, 10)
wall11 = Walls((0,0,0), 560, 170, 10, 210)
wall12 = Walls((0,0,0), 440, 160, 130, 10)
while game:
    for e in event.get():
        if e.type == QUIT:
            game = False

    if finish != True:
        wind.blit(background, (0,0))
        player.reset()
        spike.reset()
        spike2.reset()
        treasure.reset()
        wall.draw_wall()
        wall2.draw_wall()
        wall3.draw_wall()
        wall4.draw_wall()
        wall5.draw_wall()
        wall6.draw_wall()
        wall7.draw_wall()
        wall8.draw_wall()
        if unlock != True:
            wall9.draw_wall()
            doorkey.reset()
        wall10.draw_wall()
        wall11.draw_wall()
        wall12.draw_wall()
        player.step()
        spike.movement_side(110, 270)
        spike2.movement_down(160, 320)

        if sprite.collide_rect(player, wall12) or sprite.collide_rect(player, wall) or sprite.collide_rect(player, wall2) or sprite.collide_rect(player, wall3) or sprite.collide_rect(player, wall4) or sprite.collide_rect(player, wall5) or sprite.collide_rect(player, wall6) or sprite.collide_rect(player, wall7) or sprite.collide_rect(player, wall8) or sprite.collide_rect(player, wall9) or sprite.collide_rect(player, wall10) or sprite.collide_rect(player, spike) or sprite.collide_rect(player, spike2) or sprite.collide_rect(player, wall11):
            kick.play()
            finish = True

        if sprite.collide_rect(player, doorkey):
            unlock = True

    clock.tick(FPS)
    display.update()
