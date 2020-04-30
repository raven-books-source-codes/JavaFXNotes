JAVA FX：

## 1. 核心概念

Stage

Scene

Layoutpane

Componet



javaFX程序入口是start，main方法非必须。

## 2. 一些example

1. 添加alt+快捷键。 -- Mnemonics
2. 添加Tooltip， 鼠标悬停显示提示
3. CSS添加样式

## 3. layout panes

JavaFX has the following built-in layout panes:

- AbsoluteLayout:

  ```java
  Pane root = new Pane();
  Rectangle rect = new Rectangle(25, 25, 50, 50);
  rect.setFill(Color.CADETBLUE);
  Line line = new Line(90, 40, 230, 40);
  line.setStroke(Color.BLACK);
  Circle circle = new Circle(130, 130, 30);
  circle.setFill(Color.CHOCOLATE);
  
  root.getChildren().addAll(rect, line, circle);
  Scene scene = new Scene(root, 250, 220, Color.WHITESMOKE);
  ```

- `FlowPane` – lays out its children in a flow that wraps at the flowpane's boundary.

  ```java
  private void initUI(Stage stage) {
  
      FlowPane root = new FlowPane(Orientation.HORIZONTAL, 5, 5);		// row
      root.setPadding(new Insets(5));
      
      for (int i=1; i<=100; i++) {
          root.getChildren().add(new Button(String.valueOf(i)));
      }
  
      Scene scene = new Scene(root, 300, 250);
  
      stage.setTitle("FlowPane");
      stage.setScene(scene);
      stage.show();
  }
  ```

  ![image-20200429095238295](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429095238295.png)

- `HBox` – arranges its content nodes horizontally in a single row.

  ```java
      private void initUI(Stage stage) {
  
          HBox root = new HBox(5);
          root.setPadding(new Insets(10));
          root.setAlignment(Pos.BASELINE_RIGHT);
          
          Button prevBtn = new Button("Previous");
          Button nextBtn = new Button("Next");
          Button cancBtn = new Button("Cancel");
          Button helpBtn = new Button("Help");
          
          root.getChildren().addAll(prevBtn, nextBtn, cancBtn, helpBtn);
  
          Scene scene = new Scene(root);
          stage.setTitle("Row of buttons");
          stage.setScene(scene);
          stage.show();
      }
  ```

  ![image-20200429095622376](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429095622376.png)

- `VBox` – arranges its content nodes vertically in a single column.

- `AnchorPane` – anchor nodes to the top, bottom, left side, or center of the pane.

  ```java
     private void initUI(Stage stage) {
          AnchorPane root = new AnchorPane();
         
          Button okBtn = new Button("OK");
          Button closeBtn = new Button("Close");
          HBox hbox = new HBox(5, okBtn, closeBtn);
  
          root.getChildren().addAll(hbox);
          // set hbox
          AnchorPane.setRightAnchor(hbox, 10d);
          AnchorPane.setBottomAnchor(hbox, 10d);
  
          Scene scene = new Scene(root, 300, 200);
  
          stage.setTitle("Corner buttons");
          stage.setScene(scene);
          stage.show();
      }
  ```

- `BorderPane` – lays out its content nodes in the top, bottom, right, left, or center region.

  ```java
      private void initUI(Stage stage) {
  
          root = new BorderPane();
  
          root.setTop(getTopLabel());
          root.setBottom(getBottomLabel());
          root.setLeft(getLeftLabel());
          root.setRight(getRightLabel());
          root.setCenter(getCenterLabel());
  
          Scene scene = new Scene(root, 350, 300);
          
          stage.setTitle("BorderPane");
          stage.setScene(scene);
          stage.show();
      }
  ```

  ![image-20200429095941963](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429095941963.png)

- `StackPane` – places its content nodes in a back-to-front single stack.

  

- `TilePane` – places its content nodes in uniformly sized layout cells or tiles.

- `GridPane` – places its content nodes in a grid of rows and columns.

  ​	GridPane是最灵活的布局：

  ```java
   private void initUI(Stage stage) {
          GridPane root = new GridPane();
          root.setHgap(8);
          root.setVgap(8);
          root.setPadding(new Insets(5));
          
          ColumnConstraints cons1 = new ColumnConstraints();
          cons1.setHgrow(Priority.NEVER);
  //        root.getColumnConstraints().add(cons1);
  
          ColumnConstraints cons2 = new ColumnConstraints();
          cons2.setHgrow(Priority.ALWAYS);
          
          root.getColumnConstraints().addAll(cons1, cons2);
          
          RowConstraints rcons1 = new RowConstraints();
          rcons1.setVgrow(Priority.NEVER);
          
          RowConstraints rcons2 = new RowConstraints();
          rcons2.setVgrow(Priority.ALWAYS);  
          
          root.getRowConstraints().addAll(rcons1, rcons2);
          
          Label lbl = new Label("Name:");
          TextField field = new TextField();
          ListView view = new ListView();
          Button okBtn = new Button("OK");
          Button closeBtn = new Button("Close");
  
          GridPane.setHalignment(okBtn, HPos.RIGHT);
  
          root.add(lbl, 0, 0);
          root.add(field, 1, 0, 3, 1);
          root.add(view, 0, 1, 4, 2);
          root.add(okBtn, 2, 3);
          root.add(closeBtn, 3, 3);
          
          Scene scene = new Scene(root, 280, 300);
  
          stage.setTitle("New folder");
          stage.setScene(scene);
          stage.show();
      }
  ```

![image-20200429101726805](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429101726805.png)

- MigPane

  第三方库，功能强大：

  ```xml
  <dependency>
      <groupId>com.miglayout</groupId>
      <artifactId>miglayout-javafx</artifactId>
      <version>4.2</version>
  </dependency>
  ```

  

  ```java
  /**
   * ZetCode JavaFX tutorial
   *
   * This program creates a Windows layout with 
   * a MigPane.
   *
   * Author: Jan Bodnar
   * Website: zetcode.com
   * Last modified: June 2015
   */
  
  public class MigLayoutWindowsEx extends Application {
  
      MigPane root;
      
      @Override
      public void start(Stage stage) {
  
          initUI(stage);
      }
  
      private void initUI(Stage stage) {
  
          root = new MigPane("", "[grow][]", "[][][grow][]");
          Scene scene = new Scene(root);
  
          Label lbl = new Label("Windows");
          Button actBtn = new Button("Activate");
          Button closeBtn = new Button("Close");
          Button okBtn = new Button("OK");
          Button helpBtn = new Button("Help");
          ListView listView = new ListView();
          
          createLayout(lbl, listView, actBtn, closeBtn, helpBtn, okBtn);
          
          stage.setTitle("Windows");
          stage.setScene(scene);
          stage.show();
      }
      
      private void createLayout(Control...arg) {
          
          root.add(arg[0], "wrap");
          root.add(arg[1], "w 200, h 200, span 2 2, grow");
          root.add(arg[2], "wrap");
          root.add(arg[3], "top, wrap");
          root.add(arg[4]);
          root.add(arg[5], "skip");    
      }
  
      public static void main(String[] args) {
          launch(args);
      }
  }
  ```

## 4.JAVAFX Controls

- Label，文本显示。

  可以使用LabelFor属性，将Label和其他控件绑定在一起。

- CheckBox， 复选框

  ```java
  private void initUI(Stage stage) {
  
      HBox root = new HBox();
      root.setPadding(new Insets(10, 0, 0, 10));
  
      CheckBox cbox = new CheckBox("Show title");
      cbox.setSelected(true);
  
      cbox.setOnAction((ActionEvent event) -> {
          if (cbox.isSelected()) {
              stage.setTitle("CheckBox");
          } else {
              stage.setTitle("");
          }
      });
  
      root.getChildren().add(cbox);
  
      Scene scene = new Scene(root, 300, 200);
  
      stage.setTitle("CheckBox");
      stage.setScene(scene);
      stage.show();
  }
  ```

  ![image-20200429103829724](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429103829724.png)

- Slider

  ```java
  private void initUI(Stage stage) {
  
      HBox root = new HBox(10);
      root.setAlignment(Pos.CENTER);
      root.setPadding(new Insets(15));
  
      voiceLabel = new Label();
  
      Slider slider = new Slider(0, 100, 0);
      slider.valueProperty().addListener(new MyChangeListener());
      root.getChildren().addAll(slider, voiceLabel);
  
      Scene scene = new Scene(root,500,200);
  
      stage.setTitle("Slider");
      stage.setScene(scene);
      stage.show();
  }
  ```

  ![image-20200429105640443](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429105640443.png)

- ChoiceBoxEx

  ![image-20200429105720091](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429105720091.png)

- ProgressBar

  ```java
  private void initUI(Stage stage) {
  
      HBox root = new HBox(15);
      root.setAlignment(Pos.CENTER);
      root.setPadding(new Insets(10));
  
      ProgressBar pbar = new ProgressBar(0);
      pbar.setPrefWidth(150);
  
      KeyFrame frame1 = new KeyFrame(Duration.ZERO,
              new KeyValue(pbar.progressProperty(), 0));
  
      KeyFrame frame2 = new KeyFrame(Duration.seconds(10),
              new KeyValue(pbar.progressProperty(), 1));
  
      Timeline task = new Timeline(frame1, frame2);
  
      Button btn = new Button("Start");
      btn.setOnAction((ActionEvent actionEvent) -> task.playFromStart());
  
      root.getChildren().addAll(pbar, btn);
  
      Scene scene = new Scene(root);
  
      stage.setTitle("ProgressBar");
      stage.setScene(scene);
      stage.show();
  }
  ```

  ![image-20200429110038156](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429110038156.png)

  - DatePicker 日期选择器
  
    ```java
    private void initUI(Stage stage) {
    
        VBox root = new VBox(15);
        root.setPadding(new Insets(10));
    
        Label lbl = new Label("...");
    
        DatePicker datePicker = new DatePicker();
    
        datePicker.setOnAction(e -> {
    
            LocalDate date = datePicker.getValue();
            lbl.setText(date.toString());
        });
    
        root.getChildren().addAll(datePicker, lbl);
    
        Scene scene = new Scene(root, 350, 200);
    
        stage.setTitle("Date picker");
        stage.setScene(scene);
        stage.show();
    }
    ```
  
    ![image-20200429110403626](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429110403626.png)
  
    - MenuBar
  
      ```java
      private void initUI(Stage stage) {
      
          HBox root = new HBox();
      
          MenuBar mbar = new MenuBar();
          mbar.prefWidthProperty().bind(stage.widthProperty());
      
          MyMenuHandler handler = new MyMenuHandler();
      
          Menu fileMenu = new Menu("File");
          mbar.getMenus().add(fileMenu);
      
          MenuItem nmi = new MenuItem("New");
          nmi.setOnAction(handler);
          fileMenu.getItems().add(nmi);
      
          MenuItem omi = new MenuItem("Open");
          omi.setOnAction(handler);
          fileMenu.getItems().add(omi);
      
          MenuItem smi = new MenuItem("Save");
          smi.setOnAction(handler);
          fileMenu.getItems().add(smi);
      
          fileMenu.getItems().add(new SeparatorMenuItem());
      
          MenuItem emi = new MenuItem("Exit");
          emi.setOnAction((ActionEvent event) -> Platform.exit());
      
          fileMenu.getItems().add(emi);
      
          root.getChildren().add(mbar);
      
          Scene scene = new Scene(root, 300, 250);
      
          stage.setTitle("MenuBar");
          stage.setScene(scene);
          stage.show();
      }
      ```

![image-20200429111323010](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429111323010.png)

- ColorPicker

  ```java
  private void initUI(Stage stage) {
  
      HBox root = new HBox(25);
      root.setAlignment(Pos.BASELINE_CENTER);
      root.setPadding(new Insets(10));
  
      Text txt = new Text("ZetCode");
  
      Font font = Font.font(20);
      txt.setFont(font);
  
      ColorPicker cp = new ColorPicker();
      cp.setOnAction((ActionEvent event) -> txt.setFill(cp.getValue()));
  
      root.getChildren().addAll(cp, txt);
  
      Scene scene = new Scene(root, 300, 250);
  
      stage.setTitle("ColorPicker");
      stage.setScene(scene);
      stage.show();
  }
  ```

![image-20200429111828563](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429111828563.png)

- Radio Button

  ```java
  private void initUI(Stage stage) {
  
      AnchorPane root = new AnchorPane();
  
      VBox vbox = new VBox(10);
      vbox.setPadding(new Insets(10));
  
      Label lbl1 = new Label("Difficulty");
  
      lbl2 = new Label("");
      lbl2.setStyle("-fx-background-color:wheat; -fx-padding: 0 0 0 5");
      lbl2.prefWidthProperty().bind(stage.widthProperty().subtract(2 * BORDER));
  
      ToggleGroup tg = new ToggleGroup();
      tg.selectedToggleProperty().addListener(new MyToggleListener());
  
      RadioButton rb1 = new RadioButton("Easy");
      rb1.setToggleGroup(tg);
      rb1.setSelected(true);
  
      RadioButton rb2 = new RadioButton("Medium");
      rb2.setToggleGroup(tg);
  
      RadioButton rb3 = new RadioButton("Hard");
      rb3.setToggleGroup(tg);
  
      vbox.getChildren().addAll(lbl1, rb1, rb2, rb3);
      root.getChildren().addAll(vbox, lbl2);
  
      AnchorPane.setTopAnchor(vbox, BORDER);
      AnchorPane.setBottomAnchor(lbl2, BORDER);
      AnchorPane.setLeftAnchor(lbl2, BORDER);
  
      Scene scene = new Scene(root, 300, 250);
  
      stage.setTitle("RadioButton");
      stage.setScene(scene);
      stage.show();
  }
  ```

  ![image-20200429111850458](https://cdn.jsdelivr.net/gh/ravenxrz/PicBed/img/image-20200429111850458.png)

- TabPane

  ```java
  import javafx.application.Application;
  import javafx.scene.Scene;
  import javafx.scene.control.Tab;
  import javafx.scene.control.TabPane;
  import javafx.scene.layout.StackPane;
  import javafx.scene.paint.Color;
  import javafx.scene.shape.Circle;
  import javafx.scene.shape.Line;
  import javafx.scene.shape.Rectangle;
  import javafx.stage.Stage;
  
  public class TabPaneEx extends Application {
  
      @Override
      public void start(Stage stage) {
  
          initUI(stage);
      }
  
      private void initUI(Stage stage) {
  
          var root = new StackPane();
          var tabPane = new TabPane();
  
          var tab1 = new Tab();
          tab1.setText("Rectangle");
          tab1.setContent(new Rectangle(100, 100, Color.LIGHTSTEELBLUE));
  
          var tab2 = new Tab();
          tab2.setText("Line");
          tab2.setContent(new Line(0, 0, 100, 100));
  
          var tab3 = new Tab();
          tab3.setText("Circle");
          tab3.setContent(new Circle(0, 0, 50));
  
          tabPane.getSelectionModel().select(1);
          tabPane.getTabs().addAll(tab1, tab2, tab3);
  
          root.getChildren().add(tabPane);
  
          var scene = new Scene(root, 300, 250);
  
          stage.setTitle("TabPane");
          stage.setScene(scene);
          stage.show();
      }
  
      public static void main(String[] args) {
          launch(args);
      }
  }
  ```

- TabPane

  ```java
      private void initUI(Stage stage) {
  
          StackPane root = new StackPane();
          TabPane tabPane = new TabPane();
  
          Tab tab1 = new Tab();
          tab1.setText("Rectangle");
          tab1.setContent(new Rectangle(100, 100, Color.LIGHTSTEELBLUE));
  
          Tab tab2 = new Tab();
          tab2.setText("Line");
          tab2.setContent(new Line(0, 0, 100, 100));
  
          Tab tab3 = new Tab();
          tab3.setText("Circle");
          tab3.setContent(new Circle(0, 0, 50));
  
          tabPane.getSelectionModel().select(1);
          tabPane.getTabs().addAll(tab1, tab2, tab3);
  
          root.getChildren().add(tabPane);
  
          Scene scene = new Scene(root, 300, 250);
  
          stage.setTitle("TabPane");
          stage.setScene(scene);
          stage.show();
      }
  ```

  ## 5. Event

  Javafx 中的每个事件都有三个属性:

  - Event source 事件来源
  - Event target 活动目标
  - Event type 事件类型



exmaple:

```java
private void initUI(Stage stage) {

    HBox root = new HBox();

    ContextMenu conMenu = new ContextMenu();
    MenuItem noopMi = new MenuItem("No op");
    MenuItem exitMi = new MenuItem("Exit");

    conMenu.getItems().addAll(noopMi, exitMi);

    exitMi.setOnAction(event -> Platform.exit());

    root.setOnMousePressed(event -> {
        if (event.isSecondaryButtonDown()) {
            conMenu.show(root, event.getScreenX(),
                    event.getScreenY());
        }
    });

    Scene scene = new Scene(root, 300, 250);

    stage.setTitle("EventHandler");
    stage.setScene(scene);
    stage.show();
}
```

![image-20200429121903225](C:\Users\Raven\Pictures\blog\image-20200429121903225.png)

鼠标右键后显示contextMenu；

- 事件属性

  ```java
  private void initUI(Stage stage) {
  
      Pane root = new Pane();
  
      Rectangle rect = new Rectangle(30, 30, 80, 80);
      rect.setOnMouseClicked(e -> {
  
          System.out.println(e.getSource());
          System.out.println(e.getTarget());
          System.out.println(e.getEventType());
          System.out.format("x:%f, y:%f%n", e.getSceneX(), e.getSceneY());
          System.out.format("x:%f, y:%f%n", e.getScreenX(), e.getScreenY());
      });
  
      root.getChildren().addAll(rect);
  
      Scene scene = new Scene(root, 300, 250);
  
      stage.setTitle("Event properties");
      stage.setScene(scene);
      stage.show();
  }
  ```

- 通用handler处理器

  ```java
  private void initUI(Stage stage) {
  
      StackPane root = new StackPane();
  
      Button btn = new Button("Button");
      btn.addEventHandler(EventType.ROOT, new GenericHandler());
  
      root.getChildren().add(btn);
  
      Scene scene = new Scene(root, 300, 250);
  
      stage.setTitle("Generic handler");
      stage.setScene(scene);
      stage.show();
  }
  
  public static void main(String[] args) {
      launch(args);
  }
  
  private class GenericHandler implements EventHandler<Event> {
  
      @Override
      public void handle(Event event) {
  
          System.out.println(event.getEventType());
      }
  }
  ```

  - Timer计时器

  - 监听窗口postion

    ```java
    public class MovingWindowEx extends Application {
    
        int x = 0;
        int y = 0;
        Label lbl_x;
        Label lbl_y;
    
        @Override
        public void start(Stage stage) {
    
            initUI(stage);
        }
    
        private void initUI(Stage stage) {
    
            VBox root = new VBox(10);
            root.setPadding(new Insets(10));
    
            String txt1 = String.format("x: %d", x);
            lbl_x = new Label(txt1);
    
            String txt2 = String.format("y: %d", y);
            lbl_y = new Label(txt2);
    
            root.getChildren().addAll(lbl_x, lbl_y);
    
            stage.xProperty().addListener(new ChangeListener<Number>() {
    
                @Override
                public void changed(ObservableValue observable, Number oldValue, Number newValue) {
                    doChange( newValue);
                }
    
    
                private void doChange(Number newValue) {
    
                    x = newValue.intValue();
                    updateXLabel();
                }
    
            });
    
            stage.yProperty().addListener(new ChangeListener<Number>() {
    
                @Override
                public void changed(ObservableValue observable, Number oldValue, Number newValue) {
                    doChange((Number) newValue);
                }
    
                private void doChange(Number newValue) {
                    y = newValue.intValue();
                    updateYLabel();
                }
    
            });
    
            Scene scene = new Scene(root, 300, 250);
    
            stage.setTitle("Moving window");
            stage.setScene(scene);
            stage.show();
        }
    
        private void updateXLabel() {
    
            String txt = String.format("x: %d", x);
            lbl_x.setText(txt);
        }
    
        private void updateYLabel() {
            String txt = String.format("y: %d", y);
            lbl_y.setText(txt);
        }
    
        public static void main(String[] args) {
            launch(args);
        }
    }
    ```

  