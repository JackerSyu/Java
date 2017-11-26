### 加入JFrame的windowClosing事件中

//---------------------------------------------
//關閉視窗的確認	
//---------------------------------------------    
@Override
public void windowClosing(WindowEvent e){
    int result=JOptionPane.showConfirmDialog(this, "是否確定離開?", "確定", JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);
        
    if (result==JOptionPane.YES_OPTION){
        this.dispose();
        System.exit(0);  
    }else{
        this.setDefaultCloseOperation(WindowConstants.DO_NOTHING_ON_CLOSE);
    }            
}
//---------------------------------------------
