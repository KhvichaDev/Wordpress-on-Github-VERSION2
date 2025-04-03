# Wordpress on Github Codespace

# WordPress + phpMyAdmin Devcontainer

ეს პროექტი უზრუნველყოფს მზა სამუშაო გარემოს WordPress-ისა და phpMyAdmin-ისთვის GitHub Codespaces-ში. ის ავტომატურად აკონფიგურირებს საჭირო სერვისებს და გარემოს თქვენი WordPress პროექტის სწრაფად დასაწყებად.

## აღწერა

ეს devcontainer-ის კონფიგურაცია იყენებს Docker-ს, რათა შექმნას კონტეინერი, რომელშიც გაშვებულია:

* **Apache:** ვებ სერვერი WordPress-ისთვის.
* **MySQL:** მონაცემთა ბაზის სერვერი WordPress-ისა და phpMyAdmin-ისთვის.
* **phpMyAdmin:** ვებ-ზე დაფუძნებული ინტერფეისი MySQL-ის სამართავად.
* **WP-CLI:** ბრძანების ხაზის ინსტრუმენტი WordPress-ის სამართავად.

კონფიგურაცია ავტომატურად ასრულებს შემდეგ ნაბიჯებს კონტეინერის გაშვებისას:

1.  იწყებს MySQL და Apache სერვისებს.
2.  აკონფიგურირებს MySQL-ის root მომხმარებელს და ქმნის საჭირო მონაცემთა ბაზებს (`wp_db`, `phpmyadmin`) და მომხმარებლებს (`wp_user`, `pma`).
3.  აინსტალირებს phpMyAdmin-ის სქემას.
4.  ამოწმებს, არსებობს თუ არა WordPress-ის კონფიგურაციის ფაილი (`wp-config.php`). თუ არ არსებობს:
    * ჩამოტვირთავს WordPress-ის უახლეს ვერსიას.
    * ქმნის WordPress-ის კონფიგურაციის ფაილს მონაცემთა ბაზის დეტალებით.
    * აყენებს WordPress-ს საწყისი პარამეტრებით (სათაური, ადმინისტრატორის მომხმარებელი/პაროლი, ელფოსტა).
    * აყენებს შესაბამის ნებართვებს WordPress-ის ფაილებისთვის.
5.  ააქტიურებს Apache-ის `rewrite`, `headers` და `ssl` მოდულებს.
6.  აკონფიგურირებს Apache-ს ვირტუალურ ჰოსტს WordPress-ისთვის 80 პორტზე და phpMyAdmin-ისთვის 8080 პორტზე.

## გამოყენება

1.  დარწმუნდით, რომ გაქვთ დაინსტალირებული GitHub Codespaces გაფართოება თქვენს VS Code-ში.
2.  გახსენით თქვენი WordPress პროექტის რეპოზიტორია VS Code-ში.
3.  დააჭირეთ `Ctrl+Shift+P` (ან `Cmd+Shift+P` macOS-ზე) და აირჩიეთ "Codespaces: Create New Codespace".
4.  აირჩიეთ "Use an existing devcontainer configuration file".
5.  Codespace-ის შექმნის შემდეგ, გარემო ავტომატურად აეწყობა.
6.  WordPress ხელმისაწვდომი იქნება თქვენი Codespace-ის URL-ზე 80 პორტზე (ჩვეულებრივ, ავტომატურად იხსნება).
7.  phpMyAdmin ხელმისაწვდომი იქნება თქვენი Codespace-ის URL-ზე 8080 პორტზე.

## პორტები

* **80:** WordPress
* **8080:** phpMyAdmin

## წინაპირობები

* GitHub-ის ანგარიში
* VS Code დაინსტალირებული
* GitHub Codespaces გაფართოება VS Code-ში

## კონფიგურაცია

* `.devcontainer/devcontainer.json`: შეიცავს Codespace-ის კონფიგურაციის პარამეტრებს, როგორიცაა Docker-ის build-ის პარამეტრები, სამუშაო დირექტორია, პორტების გადამისამართება და post-create ბრძანებები.
* `.devcontainer/Dockerfile`: გამოიყენება Docker-ის image-ის შესაქმნელად, რომელიც შეიცავს საჭირო პროგრამულ უზრუნველყოფას (Ubuntu, Apache, MySQL, PHP, phpMyAdmin, WP-CLI).

## დამატებითი ინფორმაცია

* **WordPress:** [https://wordpress.org/](https://wordpress.org/)
* **phpMyAdmin:** [https://www.phpmyadmin.net/](https://www.phpmyadmin.net/)
* **WP-CLI:** [https://wp-cli.org/](https://wp-cli.org/)
* **GitHub Codespaces:** [https://github.com/features/codespaces](https://github.com/features/codespaces)

---
