#before running code. you must need to know few things. first the game plot: u need to suevive 30s to win thww game
#and second u need to change links address and i have uploaded required files for game. so, check it and change it
#surface1 = Bg image
#surf2 = Dragon
#surf3 = Baki
#surf4 = fireball
#font = style
#bg_music = bg_music
#winsurf = Riasgremory
import pygame
from sys import exit
start = 0
def display():
    Current_Time = int(pygame.time.get_ticks() / 1000 - start )
    text = font.render(f'{Current_Time}', True, 'black')  
    text_rect = text.get_rect(center=(482.5, 60))  
    win.blit(text, text_rect)
 
pygame.init()
win = pygame.display.set_mode((965,550))
pygame.display.set_caption('Get Your Waifu')
clock = pygame.time.Clock()


#Links
surface1 = pygame.image.load(r"C:\Users\Kumara\Desktop\game\Bg.jpg")
surf2 = pygame.image.load(r"C:\Users\Kumara\Desktop\game\Dragon.png")
surf3 = pygame.image.load(r"C:\Users\Kumara\Desktop\game\Baki.png")
surf4 = pygame.image.load(r"C:\Users\Kumara\Desktop\game\Fire ball.png")
winsurf = pygame.image.load(r"C:\Users\Kumara\Desktop\game\Riasgremory.png")
bg_music = pygame.mixer.Sound(r"C:\Users\Kumara\Desktop\game\Bg_music.mp3")
font = pygame.font.Font(r"C:\Users\Kumara\Desktop\game\Style.TTF",30)


winsurf = pygame.transform.scale(winsurf, (200,270))
winsurf_rect = winsurf.get_rect(center=(482.5,275))
surf3 = pygame.transform.scale(surf3, (120,270))
surf3 = pygame.transform.flip(surf3,True,False)
surf3_rect = surf3.get_rect(topleft = (70,230))
surf2 = pygame.transform.scale(surf2,(400,500))
surf4 = pygame.transform.scale(surf4,(100,35))
surf4_rect = surf4.get_rect(midleft = (550,400))
text1 = font.render('You  Died  Press  Small  r   to  Retry',True,'black')
text2 = font.render('Press  Spacebar  to  jump',True,'black')
text_rect2 = text1.get_rect(midtop=(550,25 ))  
text_rect1 = text1.get_rect(center=(482.5,275 ))  
text3 = font.render('You   Won   Rias   gremory',True,'black')
text4 = font.render('press   E   to   exit',True,'black')
text_rect3 = text1.get_rect(midtop=(550,100))  
text_rect4 = text1.get_rect(midtop=(620,450)) 




surf3_grav = 0
game_active = True



while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()
        if event.type == pygame.KEYDOWN:
            if event.key ==  pygame.K_SPACE:
                surf3_grav = -25
            if event.key ==  pygame.K_r and surf3_rect.colliderect(surf4_rect):
                game_active = True
                surf4_rect.right = 550
            if event.key == pygame.K_e and game_active == False:
                exit()




    
    if game_active == True:
        win.blit(surface1,((0,0)))
        bg_music.play()
        display()
        win.blit(text2, text_rect2)

        surf4_rect.x -= 2
        if surf4_rect.right <= 0:
            surf4_rect.right = 550

    
        
        win.blit(surf4,(surf4_rect))

        win.blit(surf2,((550,50)))
        surf3_grav += 1
        surf3_rect.y += surf3_grav
        if surf3_rect.y >= 230:
            surf3_rect.y = 230
        if surf3_rect.y <=0:
            surf3_rect.y = 0
        win.blit(surf3,surf3_rect)
        print(surf4_rect.colliderect(surf3_rect))
        key = pygame.key.get_pressed()
        if surf3_rect.colliderect(surf4_rect):
            game_active=False
            start = int(pygame.time.get_ticks()/1000)
            win.fill('#7AEC98')
            win.blit(text1, text_rect1)


        if int(pygame.time.get_ticks()/1000)-start >= 30:
            win.fill('#7AEC98')
            game_active = False
            win.blit(winsurf,winsurf_rect)
            win.blit(text3,text_rect3)
            win.blit(text4,text_rect4)
    
    

    pygame.display.update()
    clock.tick(60)
