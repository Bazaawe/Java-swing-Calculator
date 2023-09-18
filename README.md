# Java-swing-Calculator
package calculator;
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator implements ActionListener{
    
    JFrame frm;
    JTextField textfield;
    JButton[] numberBtn = new JButton[10];//this holds numbers from 0 to 10. anonymous buttons(functions)
    JButton[] functionBtn = new JButton[8];
    //The following names of the buttons are for the above functionBtn arrays
    JButton addBtn, subBtn, mulBtn, divBtn,decBtn, equBtn, delBtn, clrBtn/*, negBtn*/;
    JPanel panel;
    
    //fonts for the buttons
    Font myFont = new Font("Arial",Font.BOLD,30);
    
    double num1 = 0, num2 = 0,result = 0;
    char operator;
    
    Calculator(){
        frm = new JFrame("Calculator");
        frm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frm.setSize(420, 550);
        frm.setLayout(null);
        
        textfield = new JTextField();
        textfield.setBounds(50, 25, 300, 50);
        textfield.setFont(myFont);
        textfield.setEditable(false);//prevent the user from directly editing the textfield
        
        //Adding the buttons
        addBtn = new JButton("+");subBtn = new JButton("-");
        mulBtn = new JButton("*");divBtn = new JButton("/");
        decBtn = new JButton(".");equBtn = new JButton("=");
        delBtn = new JButton("Delete");clrBtn = new JButton("Clear");
       // negBtn = new JButton("(-)");
        
        //adding the above button objects to the functionBtn array
        functionBtn[0] = addBtn; functionBtn[1] = subBtn;
        functionBtn[2] = mulBtn; functionBtn[3] = divBtn;
        functionBtn[4] = decBtn; functionBtn[5] = equBtn;
        functionBtn[6] = delBtn; functionBtn[7] = clrBtn;
       // functionBtn[8] = negBtn;
        
        for(int i=0;i<8;i++){
           functionBtn[i].addActionListener(this);
           functionBtn[i].setFont(myFont);
           functionBtn[i].setFocusable(false);
        }
        
        for(int i=0;i<10;i++){
           numberBtn[i] = new JButton(String.valueOf(i));
           numberBtn[i].addActionListener(this);
           numberBtn[i].setFont(myFont);
           numberBtn[i].setFocusable(false);
        }
        
        //negBtn.setBounds(50, 430, 100, 50);
        delBtn.setBounds(50, 430, 145, 50);
        clrBtn.setBounds(205, 430, 150, 50);
        
        panel = new JPanel();
        panel.setBounds(50, 100, 300, 300);
        panel.setLayout(new GridLayout(4, 4, 10, 10));
        
        panel.add(numberBtn[1]); panel.add(numberBtn[2]); panel.add(numberBtn[3]);
        panel.add(addBtn);
        panel.add(numberBtn[4]); panel.add(numberBtn[5]); panel.add(numberBtn[6]);
        panel.add(subBtn);
        panel.add(numberBtn[7]); panel.add(numberBtn[8]); panel.add(numberBtn[9]);
        panel.add(mulBtn); panel.add(decBtn); panel.add(numberBtn[0]);
        panel.add(equBtn);panel.add(divBtn);
        
        frm.add(delBtn); /*frm.add(negBtn);*/ frm.add(clrBtn);
        frm.add(textfield); frm.add(panel);
        frm.setVisible(true);
    }
    public static void main(String[] args) {
        // Object of the Calculator class
        Calculator calc = new Calculator();
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        for(int i=0;i<10;i++){
            if(e.getSource()== numberBtn[i]){
                textfield.setText(textfield.getText().concat(String.valueOf(i)));
            }
        }
        if(e.getSource()== decBtn){
                textfield.setText(textfield.getText().concat("."));
            }
        if(e.getSource()== addBtn){
            num1 = Double.parseDouble(textfield.getText());
            operator = '+';
                textfield.setText("");
            }
        if(e.getSource()== subBtn){
            num1 = Double.parseDouble(textfield.getText());
            operator = '-';
                textfield.setText("");
            }
        if(e.getSource()== mulBtn){
            num1 = Double.parseDouble(textfield.getText());
            operator = '*';
                textfield.setText("");
            }
        if(e.getSource()== divBtn){
            num1 = Double.parseDouble(textfield.getText());
            operator = '/';
                textfield.setText("");
            }
        if(e.getSource()== equBtn){
            num2 = Double.parseDouble(textfield.getText());
            
            switch(operator){
                case'+' -> result = num1 + num2;
                case'-' -> result = num1 - num2;
                case'*' -> result = num1 * num2;
                case'/' -> result = num1 / num2;
            }
            textfield.setText(String.valueOf(result));
            num1=result;
        }
        if(e.getSource()== clrBtn){
            textfield.setText("");
        }
        if(e.getSource()== clrBtn){
            textfield.setText("");
        }
        if(e.getSource()== delBtn){
            String string = textfield.getText();
            textfield.setText("");
            for(int i=0;i<string.length()-1;i++){
                textfield.setText(textfield.getText()+string.charAt(i));
            }
        }
    }   
}
