#Random Avatar on Flask Python

'
from app import app
from PIL import Image, ImageDraw, ImageFont, ImageFilter
import random

COLORS = [(229, 57, 53), (216, 27, 96), (142, 36, 170), (94, 53, 177), (57, 73, 171), (30, 136, 229), (3, 155, 229),
		   (0, 172, 193), (0, 137, 123), (67, 160, 71), (249, 168, 37), (239, 108, 0), (109, 76, 65), (84, 110, 122)]


def random_ava(username):
	width = 400
	height = 400
	font_color = 'white'
	font_size = 350
	font_file = 'app/static/arial.ttf'
	save_to = 'app/static/'
	text = username[:1]
	img_name = username + "-" + str(random.randrange(9999999)) + ".jpg"
	font = ImageFont.truetype (font_file, font_size)
	im = Image.new ( "RGB", (width,height), random.choice(COLORS) )
	draw = ImageDraw.Draw ( im )
	text_x, text_y = font.getsize(text.upper())
	x = (width - text_x)/2
	y = (height - text_y)/2 - 30
	draw.text ( (x,y), text.upper(), font=font, fill=font_color )
	im.save ( save_to + img_name )
	return img_name


@app.route('/')
@app.route('/index')
def index():
	image = random_ava("suryadi")
	return "<img src='/static/" + image + "'/>"
	
'