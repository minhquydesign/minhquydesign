---
layout: post
author: minhquy
title: SQLITE THAC TÁC VỚI DỮ LIỆU
categories: [học SQLITE, học code]
tags: [SQL, SQLITE]
excerpt_separator: <!--more-->
---
<!--more-->
Các hoạt động CRUD (Tạo, Đọc, Cập nhật, Xóa) cơ bản trong PHP bằng PDO và SQLite.

Hoạt động cơ bản
 Tạo kho lưu trữ ngân hàng dữ liệu (banco.sqlite)
```
if (!is_dir('db'))
  mkdir('db', 0755);

$db = new PDO('sqlite:db/banco.sqlite');
$db->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
$db->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE,PDO::FETCH_OBJ);
```
## Create

```
$sql = "CREATE TABLE IF NOT EXISTS usuarios (id INTEGER PRIMARY KEY, apelido TEXT, senha TEXT, email TEXT, role TEXT, acesso INTEGER, cadastro INTEGER)";

try {
  $db->exec($sql);
} catch (\PDOException $e) {
  echo "Erro ao criar tabela: " . $e->getMessage();
}
```
## Read

$sql = "SELECT id,apelido,email,role,acesso,cadastro FROM usuarios";

$query = $db->prepare($sql);
$query->execute(); 
$resultado = $query->fetchAll();  

foreach ($resultado as $usuario) {
  echo "--<br />";
  echo "ID: " . $usuario->id . "<br />";
  echo "Apelido: " . $usuario->apelido . "<br />";
  echo "E-mail: " . $usuario->email . "<br />";
  echo "Cargo: " . $usuario->role . "<br />";
}
## Update
$sql = "UPDATE usuarios SET apelido = :apelido, email = :email, role = :role WHERE id = :id";

try {
  $query = $db->prepare($sql);
  $query->bindParam(':id', $id);
  $query->bindParam(':apelido', $id);
  $query->bindParam(':email', $email);
  $query->bindParam(':role', $role);
} catch (\PDOException $e) {
  echo "Erro ao atualizar registro: " . $e->getMessage();
}
## Delete
$sql = "DELETE FROM usuarios WHERE id = :id";

try {
  $query = $db->prepare($sql);
  $query->bindParam(':id', $id);
  $query->execute();
} catch (\PDOException $e) { 
  echo "Erro ao apagar registro: " . $e->getMessage();
}
Insert
$sql = "INSERT INTO usuarios (apelido, senha, email, role, acesso, cadastro) VALUES (:apelido, :senha, :email, :role, :acesso, :cadastro)";

try {
  $query = $db->prepare($sql);
  $param = array(':apelido' => $apelido, ':senha' => $hash, ':email' => $email, ':role' => $role, ':acesso' => $acesso, ':cadastro' => $cadastro);
  $query->execute($param);
} catch (\PDOException $e) {
  echo "Erro ao inserir registro: " . $e->getMessage();
}
## Drop
$sql = "DROP TABLE IF EXISTS usuarios";
try { 
  $db->exec($drop);
} catch (\PDOException $e) {
  echo "Erro ao apagar a tabela: " . $e->getMessage();
}
Bônus
## Search
$sql = "SELECT * FROM usuarios WHERE apelido LIKE :termo OR email LIKE :termo";
$termo = "%" . $termo . "%";

try {
  $query = $db->prepare($sql);
  $query->bindParam(':termo', $termo);
  $query->execute();
  $resultado = $query->fetchAll();
} catch (\PDOException $e) {
  echo "Erro ao ao buscar por $termo: " . $e->getMessage();
}
Um único registro
$sql = "SELECT * FROM usuarios WHERE id = :id LIMIT 1";

try {
  $query = $db->prepare($sql);
  $query->bindParam(':id', $id);
  $query->execute();
  $resultado = $query->fetch();
} catch (\PDOException $e) {
  echo "Erro ao ao buscar por $termo: " . $e->getMessage();
}
Contando resultados
$sql = "SELECT * FROM usuarios";

try {
  $query = $db->prepare($sql);
  $query->execute();
  $item = $query->fetchAll(); 
  $qtd = count($item);
} catch (\PDOException $e) {
  echo "Erro ao contar resultados: " . $e->getMessage();
}
Checa se a tabela existe
$sql = "SELECT 1 FROM usuarios LIMIT 1";

try {
  $resultado = $db->query($sql);
} catch (\PDOException $e) {
  unset($e);
  $resultado = false;
}

if ($resultado !== false) {
  echo "A tabela usuarios existe.";
} else {
  echo "A tabela usuarios não existe.";
}
Lembrando que devido ao PDO::`ATTR_DEFAULT_FETCH_MODE,PDO::FETCH_OBJ` nosso resultado será um objeto no formato: $obj->nome

Espero ter ajudado.

Forte Abraço..