# Scripts.proyectoFinal
#Scripts creacion de tablas 
USE formulauno;

-- Creación de la tabla teams
CREATE TABLE `teams` (
  `id_team` int NOT NULL AUTO_INCREMENT,
  `team_name` varchar(255) NOT NULL,
  PRIMARY KEY (`id_team`),
  UNIQUE KEY `team_name` (`team_name`)
) ENGINE=InnoDB AUTO_INCREMENT=256 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla grand_prix
CREATE TABLE `grand_prix` (
  `id_grandprix` int NOT NULL AUTO_INCREMENT,
  `grandprix_name` varchar(225) NOT NULL,
  PRIMARY KEY (`id_grandprix`),
  UNIQUE KEY `grandprix_name` (`grandprix_name`)
) ENGINE=InnoDB AUTO_INCREMENT=64 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla id_drivers
CREATE TABLE `id_drivers` (
  `id_driver` int NOT NULL AUTO_INCREMENT,
  `driver_name` varchar(225) NOT NULL,
  PRIMARY KEY (`id_driver`),
  UNIQUE KEY `driver_name` (`driver_name`)
) ENGINE=InnoDB AUTO_INCREMENT=512 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla drivers_updated
CREATE TABLE `drivers_updated` (
  `Pos` int DEFAULT NULL,
  `Driver` text,
  `Nationality` text,
  `id_team` int DEFAULT NULL,
  `PTS` double DEFAULT NULL,
  `year` int DEFAULT NULL,
  `Code` text,
  `id_drivers` int NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`id_drivers`),
  KEY `id_team_idx` (`id_team`),
  CONSTRAINT `id_team` FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1661 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla fastest_laps_updated
CREATE TABLE `fastest_laps_updated` (
  `Grand_Prix` varchar(255) DEFAULT NULL,
  `Driver` text,
  `id_team` int DEFAULT NULL,
  `Time` text,
  `year` int DEFAULT NULL,
  `Code` text,
  `id_fastest_laps` int NOT NULL AUTO_INCREMENT,
  `id_grandprix` int DEFAULT NULL,
  `id_driver` int DEFAULT NULL,
  PRIMARY KEY (`id_fastest_laps`),
  KEY `id_team_idx1` (`id_team`),
  KEY `id_grandprix_idx` (`id_grandprix`),
  KEY `id_driver_idx` (`id_driver`),
  CONSTRAINT `id_driver` FOREIGN KEY (`id_driver`) REFERENCES `id_drivers` (`id_driver`),
  CONSTRAINT `id_grandprix` FOREIGN KEY (`id_grandprix`) REFERENCES `grand_prix` (`id_grandprix`),
  CONSTRAINT `id_teams` FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1088 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla teams_updated
CREATE TABLE `teams_updated` (
  `Pos` int DEFAULT NULL,
  `PTS` int DEFAULT NULL,
  `year` int DEFAULT NULL,
  `id_team` int DEFAULT NULL,
  `id_teams_updated` int NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`id_teams_updated`),
  KEY `id_team_idx` (`id_team`),
  CONSTRAINT `id_teamm` FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=694 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creación de la tabla winners
CREATE TABLE `winners` (
  `Grand_Prix` varchar(255) DEFAULT NULL,
  `Date` text,
  `Winner` text,
  `Car` text,
  `Laps` int DEFAULT NULL,
  `Time` text,
  `Name Code` text,
  `id_winners` int NOT NULL AUTO_INCREMENT,
  `id_team` int DEFAULT NULL,
  `id_drivers_win` int DEFAULT NULL,
  `id_grandprix` int DEFAULT NULL,
  PRIMARY KEY (`id_winners`),
  KEY `id_teammm_idx` (`id_team`),
  KEY `id_drivers_idx` (`id_drivers_win`),
  KEY `id_grandprixx_idx` (`id_grandprix`),
  CONSTRAINT `id_grandprixx` FOREIGN KEY (`id_grandprix`) REFERENCES `grand_prix` (`id_grandprix`),
  CONSTRAINT `id_teammm` FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1108 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `Driver_Championships` (
    `championship_id` INT NOT NULL AUTO_INCREMENT,
    `id_driver` INT,
    `year` INT,
    `championship_type` VARCHAR(50),
    `position` INT,
    PRIMARY KEY (`championship_id`),
    FOREIGN KEY (`id_driver`) REFERENCES `id_drivers` (`id_driver`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


-- Creacion de la tabla team_championships 
CREATE TABLE `Team_Championships` (
    `championship_id` INT NOT NULL AUTO_INCREMENT,
    `id_team` INT,
    `year` INT,
    `championship_type` VARCHAR(50),
    `position` INT,
    PRIMARY KEY (`championship_id`),
    FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- creacion de la tabla race results
CREATE TABLE `Race_Results` (
    `result_id` INT NOT NULL AUTO_INCREMENT,
    `id_grandprix` INT,
    `id_driver` INT,
    `id_team` INT,
    `position` INT,
    `points` DOUBLE,
    PRIMARY KEY (`result_id`),
    FOREIGN KEY (`id_grandprix`) REFERENCES `grand_prix` (`id_grandprix`),
    FOREIGN KEY (`id_driver`) REFERENCES `id_drivers` (`id_driver`),
    FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creacion de la tabla Driver_Standings 
CREATE TABLE `Driver_Standings` (
    `standing_id` INT NOT NULL AUTO_INCREMENT,
    `year` INT,
    `id_driver` INT,
    `id_team` INT,
    `points` DOUBLE,
    PRIMARY KEY (`standing_id`),
    FOREIGN KEY (`id_driver`) REFERENCES `id_drivers` (`id_driver`),
    FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creacion de la tabla Team_Standings 
CREATE TABLE `Team_Standings` (
    `standing_id` INT NOT NULL AUTO_INCREMENT,
    `year` INT,
    `id_team` INT,
    `points` DOUBLE,
    PRIMARY KEY (`standing_id`),
    FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci; 

-- Creacion de la tabla Track_Records
CREATE TABLE `Track_Records` (
    `record_id` INT NOT NULL AUTO_INCREMENT,
    `id_grandprix` INT,
    `id_driver` INT,
    `id_team` INT,
    `lap_time` TIME,
    PRIMARY KEY (`record_id`),
    FOREIGN KEY (`id_grandprix`) REFERENCES `grand_prix` (`id_grandprix`),
    FOREIGN KEY (`id_driver`) REFERENCES `id_drivers` (`id_driver`),
    FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Creacion de la tabla Pit_Stops
CREATE TABLE `Pit_Stops` (
    `pit_stop_id` INT NOT NULL AUTO_INCREMENT,
    `id_grandprix` INT,
    `id_driver` INT,
    `id_team` INT,
    `stop_number` INT,
    `stop_duration` TIME,
    PRIMARY KEY (`pit_stop_id`),
    FOREIGN KEY (`id_grandprix`) REFERENCES `grand_prix` (`id_grandprix`),
    FOREIGN KEY (`id_driver`) REFERENCES `id_drivers` (`id_driver`),
    FOREIGN KEY (`id_team`) REFERENCES `teams` (`id_team`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


 -- Tabla de Hechos: hechos_resultados_carreras
-- Esta tabla registra los resultados de cada carrera y obtiene la información principal sobre las posiciones y los puntos obtenidos.
CREATE TABLE hechos_resultados_carreras (
    result_id INT NOT NULL AUTO_INCREMENT,
    id_grandprix INT,
    id_driver INT,
    id_team INT,
    position INT,
    points DOUBLE,
    PRIMARY KEY (result_id),
    FOREIGN KEY (id_grandprix) REFERENCES grand_prix(id_grandprix),
    FOREIGN KEY (id_driver) REFERENCES id_drivers(id_driver),
    FOREIGN KEY (id_team) REFERENCES teams(id_team)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

-- Esta tabla transaccional obtiene la información sobre las paradas en boxes realizadas durante las carreras

CREATE TABLE transaccion_paradas_boxes (
    pit_stop_id INT NOT NULL AUTO_INCREMENT,
    id_grandprix INT,
    id_driver INT,
    id_team INT,
    stop_number INT,
    stop_duration TIME,
    PRIMARY KEY (pit_stop_id),
    FOREIGN KEY (id_grandprix) REFERENCES grand_prix(id_grandprix),
    FOREIGN KEY (id_driver) REFERENCES id_drivers(id_driver),
    FOREIGN KEY (id_team) REFERENCES teams(id_team)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


-- Esta tabla transaccional obtiene los récords de vuelta en las pistas y registra el tiempo de la vuelta más rápida.

CREATE TABLE transaccion_vuelta_records (
    record_id INT NOT NULL AUTO_INCREMENT,
    id_grandprix INT,
    id_driver INT,
    id_team INT,
    lap_time TIME,
    PRIMARY KEY (record_id),
    FOREIGN KEY (id_grandprix) REFERENCES grand_prix(id_grandprix),
    FOREIGN KEY (id_driver) REFERENCES id_drivers(id_driver),
    FOREIGN KEY (id_team) REFERENCES teams(id_team)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;



------------------------------------------------------------------------------------------- Scripts creacion de otros objetos ---------------------------------------------------------------------------------
use formulauno;

-- --------------------------------------------------------------- VISTAS---------------------------------------------------------- 
-- Vista para observar el total de puntos generados por equipo en victorias
CREATE VIEW total_puntos_por_equipo AS
SELECT t.id_team, SUM(pts) AS total_puntos
FROM teams_updated t, winners w
WHERE w.id_team = t.id_team
GROUP BY t.id_team
ORDER BY total_puntos DESC;

-- Vista para observar la nacionalidad de los pilotos ganadores
CREATE VIEW Nacionalidad_pilotos_ganadores AS
SELECT Nationality, w.winner, w.Date, w.Grand_Prix
FROM drivers_updated d, winners w
WHERE d.Driver = w.Winner 
ORDER BY d.Nationality;

-- Vista para mostrar el mejor tiempo de vuelta por Gran Premio
CREATE VIEW Best_Lap_Times AS
 SELECT id_grandprix, id_driver, MIN(lap_time) AS best_lap_time
FROM Track_Records
GROUP BY id_grandprix;

-- Vista para mostrar el ranking de equipos por año
CREATE VIEW Team_Rankings AS
SELECT t.id_team, t.team_name, ts.year, ts.points
 FROM Team_Standings ts
JOIN teams t ON ts.id_team = t.id_team
ORDER BY ts.year DESC, ts.points DESC;

--  Vista para mostrar el total de puntos acumulados por piloto
CREATE VIEW Total_Puntos_Por_Piloto AS
SELECT d.id_driver, d.driver_name, SUM(rr.points) AS total_puntos
FROM id_drivers d
JOIN Race_Results rr ON d.id_driver = rr.id_driver
 GROUP BY d.id_driver, d.driver_name
ORDER BY total_puntos DESC;

-- TRIGGERS----------------------------------------------------------------------------------------------
-- Trigger para actualizar la tabla 'teams' automáticamente al insertar en 'teams_updated'
DELIMITER $$
   CREATE TRIGGER after_team_info_insert
AFTER INSERT ON teams_updated
FOR EACH ROW
BEGIN
    INSERT INTO teams (id_team, team_name)
    VALUES (NEW.id_team, NEW.team_name);
END$$
DELIMITER ;

-- Trigger para actualizar la tabla 'id_drivers' automáticamente al insertar en 'drivers_updated'
DELIMITER $$
CREATE TRIGGER after_drivers_info_insert
AFTER INSERT ON drivers_updated
FOR EACH ROW
BEGIN
    INSERT INTO id_drivers (id_driver, driver_name)
    VALUES (NEW.id_drivers, NEW.Driver);
END$$
DELIMITER ;

-- Trigger para actualizar el mejor tiempo de vuelta al insertar en 'fastest_laps_updated'
DELIMITER $$
CREATE TRIGGER actualizar_mejor_vuelta
AFTER INSERT ON fastest_laps_updated
FOR EACH ROW
BEGIN
    DECLARE mejor_tiempo VARCHAR(10);
      SELECT Time INTO mejor_tiempo 
    FROM fastest_laps_updated 
    WHERE id_driver = NEW.id_driver 
     ORDER BY Time ASC 
    LIMIT 1;
    IF NEW.Time < mejor_tiempo THEN
        UPDATE fastest_laps_updated 
        SET Time = NEW.Time 
        WHERE id_driver = NEW.id_driver;
    END IF;
END$$
DELIMITER ;

-- Trigger para actualizar el ranking de ganadores al insertar en 'winners'
DELIMITER $$
CREATE TRIGGER actualizar_ranking_ganadores
AFTER INSERT ON winners
FOR EACH ROW
BEGIN
    IF EXISTS (SELECT * FROM ranking_ganadores WHERE id_driver = NEW.id_drivers_win) THEN
        UPDATE ranking_ganadores 
        SET victorias = victorias + 1 
        WHERE id_driver = NEW.id_drivers_win;
    ELSE
        INSERT INTO ranking_ganadores (id_driver, victorias) 
        VALUES (NEW.id_drivers_win, 1);
    END IF;
END$$
DELIMITER ;




-- ------------------------------------------ Stored procedures ------------------------------------------


-- Stored procedure para cargar datos completos de un piloto en 'drivers_updated'
DELIMITER $$
CREATE PROCEDURE cargar_datos_piloto(
    IN Pos INT, 
    IN Driver VARCHAR(50), 
    IN Nationality VARCHAR(15), 
    IN id_team INT, 
     IN PTS INT, 
    IN year INT, 
    IN Code VARCHAR(15), 
    IN id_drivers INT
)
BEGIN
    INSERT INTO drivers_updated(`Pos`, `Driver`, `Nationality`, `id_team`, `PTS`, `year`, `Code`, `id_drivers`)
    VALUES (Pos, Driver, Nationality, id_team, PTS, year, Code, id_drivers);
END$$
DELIMITER ;

-- Stored procedure para obtener todos los datos de un piloto utilizando su nombre
DELIMITER $$
CREATE PROCEDURE datos_piloto(IN nombre_piloto VARCHAR(50))
BEGIN 
    SELECT * FROM drivers_updated WHERE Driver = nombre_piloto;
END$$
DELIMITER ;

-- Stored procedure para obtener el mejor tiempo de vuelta por Gran Premio
DELIMITER $$
CREATE PROCEDURE GetBestLapTime(IN grandprix_id INT)
BEGIN
    SELECT id_driver, lap_time
    FROM Track_Records
     WHERE id_grandprix = grandprix_id
    ORDER BY lap_time ASC
    LIMIT 1;
END$$
DELIMITER ;

-- Stored procedure para obtener el piloto con más victorias
DELIMITER $$
CREATE PROCEDURE GetTopDriver()
BEGIN
    SELECT Winner, COUNT(*) AS victories
    FROM winners
     GROUP BY Winner
    ORDER BY victories DESC
    LIMIT 1;
END$$
DELIMITER ; 


-- ----------------------------------------------------- Funciones ------------------------------------------------------------
-- Función para contar las victorias de un piloto
DELIMITER $$
CREATE FUNCTION contar_victorias_piloto(piloto_nombre VARCHAR(50))
 RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE victorias INT;
    SELECT COUNT(*) INTO victorias
    FROM winners
    WHERE Winner = piloto_nombre;
    RETURN victorias;
END$$
DELIMITER ;

-- Función para calcular el promedio de puntos generados por un equipo
DELIMITER $$
CREATE FUNCTION promedio_puntos_equipo(id_equipo INT) 
RETURNS INT
DETERMINISTIC 
BEGIN 
    DECLARE promedio_puntos INT;
    SELECT AVG(PTS) INTO promedio_puntos
    FROM teams_updated
    WHERE id_team = id_equipo;
    RETURN promedio_puntos;
END$$
DELIMITER ;

-- Función para obtener el total de puntos de un piloto por temporada
DELIMITER $$
CREATE FUNCTION Total_Points_By_Driver(driver_id INT, season_year INT)
RETURNS DOUBLE
DETERMINISTIC
BEGIN
    DECLARE total_points DOUBLE;
    SELECT SUM(points) INTO total_points
    FROM Race_Results
    WHERE id_driver = driver_id AND YEAR(CURDATE()) = season_year;
    RETURN total_points;
END$$
DELIMITER ;

-- Función para obtener el total de puntos por equipo por temporada
DELIMITER $$
CREATE FUNCTION Total_Points_By_Team(team_id INT, season_year INT)
RETURNS DOUBLE
 DETERMINISTIC
BEGIN
    DECLARE total_points DOUBLE;
    SELECT SUM(points) INTO total_points
    FROM Race_Results
    WHERE id_team = team_id AND YEAR(CURDATE()) = season_year;
    RETURN total_points;
END$$
DELIMITER ;





