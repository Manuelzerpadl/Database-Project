-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
-- -----------------------------------------------------
-- Schema blockbuster
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema blockbuster
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `blockbuster` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `blockbuster` ;

-- -----------------------------------------------------
-- Table `blockbuster`.`customer`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `blockbuster`.`customer` (
  `customer_id` INT NOT NULL,
  `name` VARCHAR(45) NULL DEFAULT NULL,
  `lastname` VARCHAR(45) NULL DEFAULT NULL,
  `telephone` VARCHAR(45) NULL DEFAULT NULL,
  `mail` VARCHAR(100) NULL DEFAULT NULL,
  PRIMARY KEY (`customer_id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `blockbuster`.`films`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `blockbuster`.`films` (
  `film_id` INT NOT NULL,
  `title` VARCHAR(100) NULL DEFAULT NULL,
  `description` VARCHAR(1500) NULL DEFAULT NULL,
  `release_year` CHAR(4) NULL DEFAULT NULL,
  `language` VARCHAR(20) NULL DEFAULT NULL,
  `original_language` VARCHAR(20) NULL DEFAULT NULL,
  `rental_duration` INT NULL DEFAULT NULL,
  `rental_rate` DOUBLE NULL DEFAULT NULL,
  `length` BIGINT NULL DEFAULT NULL,
  `replacement_cost` FLOAT NULL DEFAULT NULL,
  `rating` VARCHAR(20) NULL DEFAULT NULL,
  `special_features` VARCHAR(200) NULL DEFAULT NULL,
  `actors` VARCHAR(250) NULL DEFAULT NULL,
  `category` VARCHAR(40) NULL DEFAULT NULL,
  PRIMARY KEY (`film_id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `blockbuster`.`inventory`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `blockbuster`.`inventory` (
  `inventory_id` INT NOT NULL,
  `film_id` INT NULL DEFAULT NULL,
  `store_id` INT NULL DEFAULT NULL,
  PRIMARY KEY (`inventory_id`),
  INDEX `fk_inventory_films1_idx` (`film_id` ASC) VISIBLE,
  CONSTRAINT `fk_inventory_films1`
    FOREIGN KEY (`film_id`)
    REFERENCES `blockbuster`.`films` (`film_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `blockbuster`.`rental`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `blockbuster`.`rental` (
  `rental_id` INT NOT NULL,
  `rental_date` VARCHAR(20) NULL DEFAULT NULL,
  `inventory_id` INT NULL DEFAULT NULL,
  `customer_id` INT NULL DEFAULT NULL,
  `return_date` VARCHAR(20) NULL DEFAULT NULL,
  `staff_id` INT NULL DEFAULT NULL,
  PRIMARY KEY (`rental_id`),
  INDEX `fk_rental_inventory_idx` (`inventory_id` ASC) VISIBLE,
  INDEX `fk_rental_customer1_idx` (`customer_id` ASC) VISIBLE,
  CONSTRAINT `fk_rental_inventory`
    FOREIGN KEY (`inventory_id`)
    REFERENCES `blockbuster`.`inventory` (`inventory_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_rental_customer1`
    FOREIGN KEY (`customer_id`)
    REFERENCES `blockbuster`.`customer` (`customer_id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
