/*
 Navicat Premium Data Transfer

 Source Server         : localhost_3306
 Source Server Type    : MySQL
 Source Server Version : 80039
 Source Host           : localhost:3306
 Source Schema         : bookshop

 Target Server Type    : MySQL
 Target Server Version : 80039
 File Encoding         : 65001

 Date: 01/09/2024 22:30:17
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for book
-- ----------------------------
DROP TABLE IF EXISTS `book`;
CREATE TABLE `book`  (
  `b_id` int NOT NULL AUTO_INCREMENT,
  `b_isbn` varchar(13) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `b_name` varchar(50) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `b_author` varchar(30) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `b_publisher` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NULL DEFAULT NULL,
  `b_cover` varchar(45) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `b_price` float NOT NULL,
  `bt_id` int NOT NULL,
  `b_stock` int NULL DEFAULT NULL,
  `b_mark` varchar(500) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NULL DEFAULT NULL,
  PRIMARY KEY (`b_id`) USING BTREE,
  UNIQUE INDEX `b_isbn`(`b_isbn` ASC) USING BTREE,
  INDEX `bt_id`(`bt_id` ASC) USING BTREE,
  CONSTRAINT `book_ibfk_1` FOREIGN KEY (`bt_id`) REFERENCES `booktype` (`bt_id`) ON DELETE RESTRICT ON UPDATE RESTRICT
) ENGINE = InnoDB AUTO_INCREMENT = 100096 CHARACTER SET = utf8mb3 COLLATE = utf8mb3_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of book
-- ----------------------------
INSERT INTO `book` VALUES (100094, '0001', '高等数学', '同济大学', '高等数学出版社', 'images/1724948729963.jpg', 30, 5, 20, '同济大学版高等数学，价格便宜，童叟无欺');
INSERT INTO `book` VALUES (100095, '0002', '百年孤独', '马尔克斯', '南海出版社', 'images/1725009218221.jpg', 26, 1, 20, '魔幻现实主义巅峰之作');
INSERT INTO `book` VALUES (100096, '0003', '人性的弱点', '戴尔·卡耐基', '天津人民出版社', 'images/1725199612385.jpg', 44, 3, 60, '心理学类作品');
INSERT INTO `book` VALUES (1000095, '0004', '时间简史', '霍金', '湖南科学技术出版社', 'images/1725198690358.jpg', 55, 2, 66, '伟大的科学著作');
INSERT INTO `book` VALUES (1000096, '0005', '艺术的故事', '贡布里希', '广西美术出版社', 'images/1725198812717.jpg', 70, 4, 51, '伟大的作品');
INSERT INTO `book` VALUES (1000097, '0006', '三体', '刘慈欣', '重庆出版社', 'images/1725199046848.jpg', 60, 1, 0, '雨果奖获得者');

-- ----------------------------
-- Table structure for booktype
-- ----------------------------
DROP TABLE IF EXISTS `booktype`;
CREATE TABLE `booktype`  (
  `bt_id` int NOT NULL AUTO_INCREMENT,
  `bt_name` varchar(30) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  PRIMARY KEY (`bt_id`) USING BTREE,
  UNIQUE INDEX `bt_name`(`bt_name` ASC) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 32 CHARACTER SET = utf8mb3 COLLATE = utf8mb3_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of booktype
-- ----------------------------
INSERT INTO `booktype` VALUES (5, '教育类');
INSERT INTO `booktype` VALUES (1, '文学类');
INSERT INTO `booktype` VALUES (3, '社会科学类');
INSERT INTO `booktype` VALUES (2, '科技类');
INSERT INTO `booktype` VALUES (4, '艺术类');

-- ----------------------------
-- Table structure for order
-- ----------------------------
DROP TABLE IF EXISTS `order`;
CREATE TABLE `order`  (
  `o_id` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `o_total` float NOT NULL,
  `o_amount` int NOT NULL,
  `o_status` int NOT NULL,
  `o_paytype` int NOT NULL,
  `u_id` int NOT NULL,
  `o_datetime` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `o_realname` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `o_phone` varchar(11) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `o_address` varchar(50) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  PRIMARY KEY (`o_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb3 COLLATE = utf8mb3_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of order
-- ----------------------------
INSERT INTO `order` VALUES ('20190828105550576', 39.8, 2, 3, 1, 8, '2019-08-28 10:55:51', '马腾飞', '18245631746', '东大软件园A10');
INSERT INTO `order` VALUES ('20190830140315412', 542.7, 3, 4, 2, 21, '2019-08-30 14:03:16', '测试用户', '13245671234', '东软实训中心A10');
INSERT INTO `order` VALUES ('20190830141454223', 260.4, 2, 2, 1, 21, '2019-08-30 14:14:55', '测试用户', '13245671234', '东软实训中心A10');
INSERT INTO `order` VALUES ('20240830171357337', 56, 2, 6, 1, 25, '2024-08-30 17:13:57', '朱士睿', '19588906940', '');
INSERT INTO `order` VALUES ('20240830201617999', 26, 1, 5, 3, 25, '2024-08-30 20:16:18', '朱士睿', '19588906940', '');
INSERT INTO `order` VALUES ('20240901173513896', 26, 1, 5, 1, 25, '2024-09-01 17:35:13', '朱士睿', '19588906940', '');
INSERT INTO `order` VALUES ('20240901212217099', 26, 1, 2, 1, 25, '2024-09-01 21:22:17', '朱士睿', '19588906940', '');
INSERT INTO `order` VALUES ('20240901212335064', 30, 1, 2, 1, 25, '2024-09-01 21:23:35', '朱士睿', '19588906940', '');

-- ----------------------------
-- Table structure for orderitem
-- ----------------------------
DROP TABLE IF EXISTS `orderitem`;
CREATE TABLE `orderitem`  (
  `oi_id` int NOT NULL AUTO_INCREMENT,
  `oi_price` float NOT NULL,
  `oi_amount` int NOT NULL,
  `b_id` int NOT NULL,
  `o_id` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  PRIMARY KEY (`oi_id`) USING BTREE,
  INDEX `o_id`(`o_id` ASC) USING BTREE,
  CONSTRAINT `orderitem_ibfk_2` FOREIGN KEY (`o_id`) REFERENCES `order` (`o_id`) ON DELETE RESTRICT ON UPDATE RESTRICT
) ENGINE = InnoDB AUTO_INCREMENT = 24 CHARACTER SET = utf8mb3 COLLATE = utf8mb3_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of orderitem
-- ----------------------------
INSERT INTO `orderitem` VALUES (8, 19.9, 2, 100057, '20190828105550576');
INSERT INTO `orderitem` VALUES (16, 233, 2, 100053, '20190830140315412');
INSERT INTO `orderitem` VALUES (17, 76.7, 1, 100007, '20190830140315412');
INSERT INTO `orderitem` VALUES (18, 27.4, 1, 100001, '20190830141454223');
INSERT INTO `orderitem` VALUES (19, 233, 1, 100053, '20190830141454223');
INSERT INTO `orderitem` VALUES (20, 26, 1, 100095, '20240830171357337');
INSERT INTO `orderitem` VALUES (21, 30, 1, 100094, '20240830171357337');
INSERT INTO `orderitem` VALUES (22, 26, 1, 100095, '20240830201617999');
INSERT INTO `orderitem` VALUES (23, 26, 1, 100095, '20240901173513896');
INSERT INTO `orderitem` VALUES (24, 26, 1, 100095, '20240901212217099');
INSERT INTO `orderitem` VALUES (25, 30, 1, 100094, '20240901212335064');

-- ----------------------------
-- Table structure for recommend
-- ----------------------------
DROP TABLE IF EXISTS `recommend`;
CREATE TABLE `recommend`  (
  `r_id` int NOT NULL AUTO_INCREMENT,
  `r_type` int NOT NULL,
  `b_id` int NOT NULL,
  PRIMARY KEY (`r_id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 72 CHARACTER SET = utf8mb3 COLLATE = utf8mb3_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of recommend
-- ----------------------------
INSERT INTO `recommend` VALUES (68, 3, 100093);
INSERT INTO `recommend` VALUES (70, 2, 100094);
INSERT INTO `recommend` VALUES (71, 2, 100095);
INSERT INTO `recommend` VALUES (73, 2, 2);
INSERT INTO `recommend` VALUES (74, 2, 100096);
INSERT INTO `recommend` VALUES (76, 2, 1);
INSERT INTO `recommend` VALUES (77, 2, 1000095);
INSERT INTO `recommend` VALUES (78, 2, 1000096);
INSERT INTO `recommend` VALUES (80, 3, 1000097);
INSERT INTO `recommend` VALUES (81, 3, 1000096);

-- ----------------------------
-- Table structure for user
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user`  (
  `u_id` int NOT NULL AUTO_INCREMENT,
  `u_name` varchar(8) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `u_pwd` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `u_realname` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `u_redgt` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `u_role` int NOT NULL,
  `u_mark` varchar(20) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NULL DEFAULT NULL,
  `u_phone` varchar(11) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  `u_address` varchar(50) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci NOT NULL,
  PRIMARY KEY (`u_id`) USING BTREE,
  UNIQUE INDEX `u_name`(`u_name` ASC) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 27 CHARACTER SET = utf8mb3 COLLATE = utf8mb3_general_ci ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of user
-- ----------------------------
INSERT INTO `user` VALUES (5, 'admin', '2jtPZkLoSG4=', '管理员', '2019-08-24 11:36:58', 0, '超级管理员', '18245631746', '东大软件园B园G1公寓');
INSERT INTO `user` VALUES (6, 'vili', 's5xphGZ7pPM=', '魏志林', '2019-08-26 09:42:42', 1, '普通用户', '18245631746', '东软实训中心A10');
INSERT INTO `user` VALUES (7, 'lxf', 'a/6fps7mep0=', '刘雪峰', '2019-08-27 09:00:06', 1, '普通用户', '18245631746', '内蒙古自治区呼和浩特市赛罕区大学西路内蒙古大学');
INSERT INTO `user` VALUES (8, 'mtf', 'i/0tfHMkhFI=', '马腾飞', '2019-08-27 09:02:50', 1, '普通用户', '18647990985', '东大软件园A10');
INSERT INTO `user` VALUES (9, 'll', 'hEVlfKYSHfk=', '刘璐', '2019-08-27 09:39:18', 1, '普通用户', '1377777777', '东大软件园A1000000');
INSERT INTO `user` VALUES (22, 'zyq', '3Ws203U8QwY=', '赵悦桥', '2019-08-30 14:53:29', 1, '普通用户', '18245631746', '东大软件园A1');
INSERT INTO `user` VALUES (25, 'lveto', 'gpCLX2H8+7w=', '朱士睿', '2024-08-29 21:11:54', 0, '普通用户', '19588906940', '');
INSERT INTO `user` VALUES (26, '222', 'gpCLX2H8+7w=', '123', '2024-08-29 21:16:38', 1, '普通用户', '', '');

SET FOREIGN_KEY_CHECKS = 1;
