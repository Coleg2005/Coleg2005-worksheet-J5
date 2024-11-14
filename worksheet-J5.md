# Worksheet 5

### Question 1. How does object-oriented programming pair so closely with GUIs?

Because it separates user interface with the code which is information hiding

### Question 2. What is the relationship between WindowListener and WindowAdapter?

WindowAdapter is the class that implements WindowListener whic is an interface

### Question 3. What does the program below produce for a GUI? (You can sketch and upload an image or describe it – do this without running the program to make sure you understand what each line below is doing).

``` java
 // For reference
    /*        N
    *         |
    *      W--|--E
    *         |
    *         S
    */
    public static void main(final String args[]) {
        JFrame frame = new JFrame();

        JButton bOne = new JButton("1");
        JButton bTwo = new JButton("2");
        JButton bThree = new JButton("3");
        JButton bFour = new JButton("4");
        JButton bFive = new JButton("5");
        JButton bSix = new JButton("6");

        JPanel primes = new JPanel();
        JPanel composites = new JPanel();

        primes.setLayout(new BorderLayout());
        composites.setLayout(new BorderLayout());

        primes.add(bTwo, BorderLayout.EAST);
        primes.add(bThree,BorderLayout.WEST);
        primes.add(bFive,BorderLayout.NORTH);

        composites.add(bFour, BorderLayout.NORTH);
        composites.add(bSix, BorderLayout.CENTER);
 
        frame.add(primes, BorderLayout.WEST);
        frame.add(composites, BorderLayout.EAST);
        frame.add(bOne, BorderLayout.CENTER);
        frame.pack();
        frame.setTitle("Quiz J4-2");
        frame.setSize(400, 400);
        frame.setLocation(100, 100);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
```

This has a title at the top saying Quiz J4-2, on the left third, 5 button on top and 3 button bottom left with 2 button bottom right and in the center thrid is a 1 button, and on the right third on the top is a 4 button and on the bottom is a 6 button


### Question 4. Modify the HelloGoodbyeEx2 code to update the number of times the button has been clicked on the button’s label itself.

``` java
import javax.swing.*;
import java.awt.*;

public class HelloGoodbyeEx2 {

    static int count;

    public static void main(String args[]) {
        JFrame f = new JFrame();
        f.setTitle("Hello/Goodbye Ex1");
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);        
        JLabel label = new JLabel("Hello");
        JButton button = new JButton("Click me! count: " + count);

        //using an anonymous (static) class
        //avoids having to make ButtonClickListenerEx1 class above
        button.addActionListener((e) -> {
            count++;
            button.setText("Click me! count: " + count);
            if (label.getText().equals("Hello")) {
                label.setText("Goodbye");
            }else {
                label.setText("Hello");
            }
        });
        
        f.add(button, BorderLayout.SOUTH);
        f.add(label, BorderLayout.NORTH);

        f.pack();
        f.setVisible(true);
        
    }
}
```

### Question 5. Consider the following Java swing GUI

``` java
public class RedPillBluePill extends JFrame {
    JLabel label;

    public RedPillBluePill() {
        this.setSize(300, 300);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel panel = new JPanel(new BorderLayout());        
        JButton red = new JButton("red");
        JButton blue = new JButton("blue");
        panel.add(red, BorderLayout.EAST);
        panel.add(blue, BorderLayout.WEST);
        label = new JLabel("click a button");
        this.add(label, BorderLayout.NORTH);
        this.add(panel, BorderLayout.SOUTH);

        blue.addActionListener((e) -> {
            label.setText("BLUE");
        });

        red.addActionListener((e) -> {
            label.setText("RED");        
        });
    }
}
```
Convert the ActionListeners to Lambda Functions.



### Question 6. Explain why for ActionListener you can use a Lambda function but for WindowListener you cannot?

Because ActionListener only has one function and WindowListener has multiple.

### Question 7. Write a program that allows you to enter a 6-digit PIN, like you would on your smartphone to unlock it. It should have the following layout:


 [ DISPLAY PIN AS TYPED ]

   [ 1 ]  [ 2 ] [ 3 ] 
   
   [ 4 ]  [ 5 ] [ 6 ]    
   
   [ 7 ]  [ 8 ] [ 9 ]       

   [ < ]  [ 0 ] 

Where [ < ] is a “backspace” button. The display should show the PIN as it is typed, and when the user enters the PIN 202113, the display changes to “YOU MAY ENTER!”

``` java
import javax.swing.*;
import java.awt.*;

public class Worksheet {

    static int index = 0;

    public static void main(String[] args) {
        JButton bOne = new JButton("1");
        JButton bTwo = new JButton("2");
        JButton bThree = new JButton("3");
        JButton bFour = new JButton("4");
        JButton bFive = new JButton("5");
        JButton bSix = new JButton("6");
        JButton bSeven = new JButton("7");
        JButton bEight = new JButton("8");
        JButton bNine = new JButton("9");
        JButton bZero = new JButton("0");
        JButton bBack = new JButton("<");

        JFrame f = new JFrame();
        GridLayout grid = new GridLayout(4, 3);
        JPanel pin = new JPanel();
        pin.setLayout(grid);

        char[] label = new char[6];
        for (int i = 0; i < 6; i++) {
            label[i] = '*';
        }
        JLabel lab = new JLabel(new String(label));

        f.add(pin, BorderLayout.SOUTH);
        f.add(lab, BorderLayout.NORTH);

        pin.add(bOne);
        pin.add(bTwo);
        pin.add(bThree);
        pin.add(bFour);
        pin.add(bFive);
        pin.add(bSix);
        pin.add(bSeven);
        pin.add(bEight);
        pin.add(bNine);
        pin.add(bZero);
        pin.add(bBack);

        bOne.addActionListener(e -> Helper(bOne, label, lab));
        bTwo.addActionListener(e -> Helper(bTwo, label, lab));
        bThree.addActionListener(e -> Helper(bThree, label, lab));
        bFour.addActionListener(e -> Helper(bFour, label, lab));
        bFive.addActionListener(e -> Helper(bFive, label, lab));
        bSix.addActionListener(e -> Helper(bSix, label, lab));
        bSeven.addActionListener(e -> Helper(bSeven, label, lab));
        bEight.addActionListener(e -> Helper(bEight, label, lab));
        bNine.addActionListener(e -> Helper(bNine, label, lab));
        bZero.addActionListener(e -> Helper(bZero, label, lab));
        bBack.addActionListener(e -> Helper(bBack, label, lab));

        f.pack();
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.setVisible(true);
    }

    public static void Helper(JButton button, char[] label, JLabel lab) {
        String buttonText = button.getText();

        if ("<".equals(buttonText)) {
            if (index > 0) {
                index--;
                label[index] = '*';
            }
        } else if (index < 6) {
            label[index] = buttonText.charAt(0);
            index++;
        }

        if("202113".equals(new String(label))) {
            System.out.println("YOU MAY ENTER!");
            lab.setText("YOU MAY ENTER!");
            return;
        }

        lab.setText(new String(label));
    }

}
```
