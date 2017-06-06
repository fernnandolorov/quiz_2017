var path = require('path');

// Cargar ORM
var Sequelize = require('sequelize');

// Para usar en local BBDD SQLite:
//    DATABASE_URL = sqlite:///
//    DATABASE_STORAGE = quiz.sqlite
// Para usar en Heroku BBDD Postgres:
//    DATABASE_URL = postgres://user:passwd@host:port/database

var url, storage;

if (!process.env.DATABASE_URL) {
    url = "postgres://peifpcidwlxzkd:5c85fe03f6f1f24dbbb1a4fcda6b336ed03bc25c1b20800db7b5e2793230668f@ec2-176-34-111-152.eu-west-1.compute.amazonaws.com:5432/de13u7k7ao47ef";
//      url = "sqlite:///";
//      storage = "quiz.sqlite";
} else {
    url = process.env.DATABASE_URL;
    storage = process.env.DATABASE_STORAGE || "";
}

var sequelize = new Sequelize(url, {storage: storage});



// Importar la definicion de la tabla Quiz de quiz.js
var Quiz = sequelize.import(path.join(__dirname, 'quiz'));


// Importar la definicion de la tabla Tips de tips.js
var Tip = sequelize.import(path.join(__dirname,'tip'));

// Importar la definicion de la tabla Users de user.js
var User = sequelize.import(path.join(__dirname,'user'));


// Relaciones entre modelos
Tip.belongsTo(Quiz);
Quiz.hasMany(Tip);

// Relacion 1 a N entre User y Quiz:
User.hasMany(Quiz, {foreignKey: 'AuthorId'});
Quiz.belongsTo(User, {as: 'Author', foreignKey: 'AuthorId'});

// Relacion 1 a N entre User y Tip:
User.hasMany(Tip, {foreignKey: 'AuthorId'});
Tip.belongsTo(User, {as: 'Author', foreignKey: 'AuthorId'});


exports.Quiz = Quiz; // exportar definición de tabla Quiz
exports.Tip = Tip;   // exportar definición de tabla Tips
exports.User = User; // exportar definición de tabla Users
