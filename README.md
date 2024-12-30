STONE_COLOR[0])
                b.append(tmp)
            stones.append(b)

        for i in range(0, 5):
            for j in range(0, 19):
                canvas.move(stones[i][j].id, 25 * j, 25 * i)

        ball = Ball(canvas, BALL_COLOR[0], pole, stones, score)
        root.update_idletasks()
        root.update()

        time.sleep(1)
        while 1:
            if pole.pauseSeconds != 1:
                try:
                    canvas.delete(m)
                    del m
                except:
                    pass
                if not ball.bottom_hit:
                    ball.draw()
                    pole.draw()
                    root.update_idletasks()
                    root.update()
                    time.sleep(0.01)
                    if ball.hit == 95:
                        canvas.create_text(250, 250, text="YOU WON !!", fill="yellow", font="Calibri 24 ")
                        root.update_idletasks()
                        root.update()
                        playing = False
                        break
                else:
                    # Play the game over sound
                    game_over_sound.play()
                    canvas.create_text(250, 250, text="GAME OVER!!", fill="red", font="Calibri 24 ")
                    root.update_idletasks()
                    root.update()
                    playing = False
                    break
            else:
                try:
                    if m == None: pass
                except:
                    m = canvas.create_text(250, 250, text="PAUSE!!", fill="green", font="Calibri 24 ")
                root.update_idletasks()
                root.update()

# Exit the game when Q is pressed
def exit_game(event):
    root.destroy()  # Close the window and exit the program

# Bind keys to start the game and exit the game
root.bind_all("<Return>", start_game)
root.bind_all("<q>", exit_game)  # Exit when Q is pressed

canvas.create_text(250, 250, text="Press Enter to start Game!!", fill="yellow", font="Calibri 18")
j = canvas.find_all()
root.mainloop()
