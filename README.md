# psyCheckerboard
/**
Demonstrates how to use a JFrame to draw things.  Adapted from: 
https://docs.oracle.com/javase/tutorial/uiswing/examples/events/index.html#MouseEventDemo


 * Copyright (c) 1995, 2008, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle or the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.


@author Pete Nordquist
@version 100218
*/
/*Author: Isaac Stoutenburgh
 * 3/15/18
 */

import java.awt.GridLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Graphics;
 
import javax.swing.*;

// MouseListener Imports
import java.awt.event.MouseListener;
import java.awt.event.MouseEvent;

public class Lab7 extends JPanel implements MouseListener {
	
	Color background = Color.white;
	int redSq = 0;
	
	//ca(color array) holds my 8x8 array
	Color[][] ca = new Color[8][8];
	
	
    // main Creates a JFrame -- think of it as the window that 'holds' the running program
    public static void main(String[] args)
    {
    	// The frame handles all the outside window work
        JFrame frame = new JFrame("Lab 7");

        // Allows the 'X' in the upper right to cause the program to exit
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
         
        //Create and set up the content pane.
        // contentPane holds a panel
        JComponent newContentPane = new Lab7();
        // DrawingDemo is a JPanel is a JComponent

        newContentPane.setOpaque(true); //content panes must be opaque
        frame.setContentPane(newContentPane);
         
        //Display the window.
        frame.pack();
		/* Causes this Window to be sized to fit the preferred size and layouts of its subcomponents. 
		The resulting width and height of the window are automatically enlarged if either of dimensions
		is less than the minimum size as specified by the previous call to the setMinimumSize method. 
		If the window and/or its owner are not displayable yet, both of them are made displayable before
		calculating the preferred size. The Window is validated after its size is being calculated.
		*/
        frame.setVisible(true);
    }

    // Constructor
    public Lab7()
    {
    	// layout the panel with an area in which to draw
        super(new GridLayout(0,1));
        
    	for(int i=0; i<ca.length; i++) {
    		for(int j=0; j<ca.length; j++) {
    			int random = (int)(Math.random()*12);
    			switch (random) {
    			case 0:
    				ca[i][j] = Color.black;
    				break;
    			case 1:
    				ca[i][j] = Color.red;
    				redSq++;
    				break;
    			case 2:
    				ca[i][j] = Color.cyan;
    				break;
    			case 3:
    				ca[i][j] = Color.yellow;
    				break;
    			case 4: 
    				ca[i][j] = Color.green;
    				break;
    			case 5:
    				ca[i][j] = Color.magenta;
    				break;
    			case 6:
    				ca[i][j] = Color.pink;
    				break;
    			case 7:
    				ca[i][j] = Color.orange;
    				break;
    			case 8:
    				ca[i][j] = Color.blue;
    				break;
    			case 9:
    				ca[i][j] = Color.lightGray;
    				break;
    			case 10:
    				ca[i][j] = Color.DARK_GRAY;
    				break;
    			case 11:
    				ca[i][j] = Color.gray;
    				break;
    			}

    		}
    	}
    	
		
		// get Graphics object, which allows you to draw on the panel
	
		// set initial size of the panel
		setPreferredSize(new Dimension(900, 800));
	
		this.addMouseListener(this);
		
		// calls paint()
		repaint();

    }

    // draws the screen
    public void paint(Graphics g)
    {
    	 int sqSz = 0;
		// Fill background
		Dimension d = getSize();
	
		// set the background color
		g.setColor(background);
		g.fillRect(0,0,d.width,d.height);
		
		if(d.width >= d.height) {
			sqSz = (d.height-50)/8;
			int x=0;
			int y=0;
			
			for(int i=0; i<ca.length; i++) {
				for(int j=0; j<ca.length; j++) {
					g.setColor(ca[i][j]);
					g.fillRect(x, y, sqSz, sqSz);
					x = (x+sqSz);
				}
				y += sqSz; 
				x = 0;
			}
		}
		else {
			sqSz = (d.width)/8;
			int x=0;
			int y=0;
			for(int i=0; i<ca.length; i++) {
				for(int j=0; j<ca.length; j++) {
					g.setColor(ca[i][j]);
					g.fillRect(x, y, sqSz, sqSz);
					x = (x+sqSz);
				}
				y += sqSz; 
				x = 0;
			}
		}
		g.setColor(Color.black);
		// draw a string w/ number of red squares
		g.drawString("There are: " + redSq + " red squares!", d.width/2, d.height-20);
    }
    
    public void mouseClicked(MouseEvent evt) {
    	
    	Dimension d = this.getSize();
    	double sqSz=0;
    	double x = evt.getX();
    	double y = evt.getY();
    	
    	//calculate square size if width is >= height
    	if(getWidth()>= getHeight()) {
    		sqSz = (d.height-50)/8; 
    	}
    	//calculate square size if height>width
    	else {
    		sqSz =(d.width)/8;   
    	}
    		
    	//convert x coordinate to array index
    	if(x <= sqSz)
    		x=0;
    	else if(x <= sqSz*2)
   			x=1;
   		else if(x <= sqSz*3)
   			x=2;
    	else if(x <= sqSz*4)
    		x=3;
   		else if(x <= sqSz*5)
   			x=4;
    	else if(x <= sqSz*6)
    		x=5;
    	else if(x <= sqSz*7)
    		x=6;
    	else if(x <= sqSz*8)
    		x=7;
    		
   		//convert y coordinate to array index
   		if(y <= sqSz)
   			y=0;
    	else if(y <= sqSz*2)
    		y=1;
    	else if(y <= sqSz*3)
    		y=2;
    	else if(y <= sqSz*4)
    		y=3;
    	else if(y <= sqSz*5)
    		y=4;
    	else if(y <= sqSz*6)
    		y=5;
    	else if(y <= sqSz*7)
    		y=6;
    	else if(y <= sqSz*8)
    		y=7;
    	
   		//change array index to hold color red that corresponds to square clicked
   		if(ca[(int)y][(int)x] != Color.red) {
   			ca[(int)y][(int)x] = Color.red;
    	//increment red square count
   			redSq++;
   		}
    	//redraw checkerboard 
    	repaint();
   	
    }// mouseClicked method

	@Override
	public void mouseEntered(MouseEvent e) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void mouseExited(MouseEvent e) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void mousePressed(MouseEvent e) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void mouseReleased(MouseEvent e) {
		// TODO Auto-generated method stub
		
	}
   
}//end of class
