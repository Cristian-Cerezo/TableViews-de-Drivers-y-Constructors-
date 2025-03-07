# TableViews-de-Drivers-y-Constructors-
MAIN:
import repositories.ConstructorsResultRepository;
import repositories.DriverResultRepository;
import repositories.QueryRepository;
import repositories.SeasonRepository;
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.layout.Background;
import javafx.scene.layout.BackgroundFill;
import javafx.scene.layout.VBox;
import javafx.scene.paint.Color;
import javafx.stage.Stage;

public class Main extends Application {

    private DriverResultRepository driverResultRepository;
    private SeasonRepository seasonRepository;
    private QueryRepository queryRepository;
    private ConstructorsResultRepository constructorsResultRepository;

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("FORMULA #1");

        driverResultRepository = new DriverResultRepository();
        seasonRepository = new SeasonRepository();
        queryRepository = new QueryRepository();
        constructorsResultRepository = new ConstructorsResultRepository();

        // Crear los botones
        Button btnConductores = new Button("CONSULTAR RESULTADOS DE LOS DRIVERS");
        btnConductores.setOnAction(e -> openConductoresWindow());
        btnConductores.setStyle("-fx-background-color: #4CAF50; -fx-text-fill: white;");

        Button btnConstructores = new Button("CONSULTAR RESULTADOS DE LOS CONSTRUCTORS");
        btnConstructores.setOnAction(e -> openConstructoresWindow());
        btnConstructores.setStyle("-fx-background-color: #2196F3; -fx-text-fill: white;");

        Button btnGraficoConductores = new Button("CONSULTAR GRAFICO DE BARRAS DE LOS DRIVERS");
        btnGraficoConductores.setOnAction(e -> openGraficoConductoresWindow());
        btnGraficoConductores.setStyle("-fx-background-color: #FFC107; -fx-text-fill: black;");

        Button btnGraficoConstructores = new Button("CONSULTAR GRAFICO DE BARRAS DE LOS CONSTRUCTORS");
        btnGraficoConstructores.setOnAction(e -> openGraficoConstructoresWindow());
        btnGraficoConstructores.setStyle("-fx-background-color: #FF5722; -fx-text-fill: white;");

        // Crear etiquetas
        Label titleLabel = new Label("RESULTADOS DE LA FORMULA #1");
        titleLabel.setStyle("-fx-font-size: 24px; -fx-font-weight: bold; -fx-text-fill: #333333;");
        
        Label instructionLabel = new Label("SELECCIONE EL DATO QUE DESEA VISUALIZAR");
        instructionLabel.setStyle("-fx-font-size: 16px; -fx-text-fill: #555555;");

        // Organizar layout
        VBox vbox = new VBox(20);
        vbox.setPadding(new Insets(50));
        vbox.getChildren().addAll(titleLabel, instructionLabel, btnConductores, btnConstructores, btnGraficoConductores, btnGraficoConstructores);

        // Establecer color de fondo para la Scene
        BackgroundFill backgroundFill = new BackgroundFill(Color.LIGHTBLUE, null, null); // Aquí puedes cambiar el color
        Background background = new Background(backgroundFill);
        vbox.setBackground(background);

        Scene scene = new Scene(vbox, 600, 400); // Ajustar el tamaño de la escena según tus necesidades
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void openConductoresWindow() {
        VentanaConductores conductoresWindow = new VentanaConductores(driverResultRepository, seasonRepository);
        conductoresWindow.start(new Stage());
    }

    private void openConstructoresWindow() {
        VentanaConstructores constructoresWindow = new VentanaConstructores(constructorsResultRepository, seasonRepository);
        constructoresWindow.start(new Stage());
    }

    private void openGraficoConductoresWindow() {
        GraficoConductores graficoConductoresWindow = new GraficoConductores(queryRepository);
        graficoConductoresWindow.start(new Stage());
    }

    private void openGraficoConstructoresWindow() {
        GraficoConstructores graficoConstructoresWindow = new GraficoConstructores(queryRepository);
        graficoConstructoresWindow.start(new Stage());
    }
}
