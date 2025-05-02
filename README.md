✅ Scopul principal
Realizarea unei clase PlayerStatus care:
•	Păstrează starea unui jucător în joc;
•	Respectă principiile OOP: incapsulare, modularitate, reutilizare, ascunderea detaliilor de implementare.
________________________________________
📦 Stare internă (atribute)

Clasa va conține:

Atribut         Tip       Descriere
-----------------------------------------------
nickname        String    Numele jucătorului (read-only)
score           int       Scorul jucătorului
lives           int       Număr de vieți
health          int       Sănătatea (0 - 100)
weaponInHand    String    Arma curentă
positionX       double    Poziția pe axa OX
positionY       double    Poziția pe axa OY
gameName        String    Numele jocului (static - comun tuturor jucătorilor)


📏 Reguli de joc importante
1.	Health:
o	Scade până la 0 → se pierde 1 viață și health revine la 100;
o	Dacă lives = 0 → Game Over;
o	health > 100 → se trunchiază la 100.
2.	Arme (weaponInHand):
o	knife (1000), sniper (10000), kalashnikov (20000);
o	Comparare arme cu .equals(), nu ==;
o	Arma poate fi cumpărată doar dacă score ≥ preț.
3.	Dueluri între jucători:
o	Dacă arme identice → probabilitate de câștig în funcție de (3 * health + score / 1000) / 4;
o	Dacă arme diferite → puterea depinde de distanță și tipul armei.
4.	Distanța:
o	Se calculează cu formula euclidiană:
(x1−x2)2+(y1−y2)2\sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}(x1−x2)2+(y1−y2)2 
________________________________________
⚙️ Metode necesare
✅ Inițializare:
•	initPlayer(nickname)
•	initPlayer(nickname, lives)
•	initPlayer(nickname, lives, score)
✅ Artefacte:
•	findArtifact(int artifactCode):
o	Cod perfect → +5000 puncte, +1 viață, health = 100;
o	Cod prim → +1000, +2 vieți, health +25;
o	Cod div. cu 3 și sumă div. cu 3 → capcană: -3000 puncte, -25 health;
o	Alt cod → +artifactCode puncte.
✅ Arme:
•	setWeaponInHand(String weapon) – setează arma dacă scorul permite.
•	getWeaponInHand() – returnează arma.
✅ Poziționare:
•	movePlayerTo(double x, double y) – actualizează poziția.
✅ Nume joc:
•	gameName – trebuie implementat ca static, acces prin getter & setter.
✅ Nume jucător:
•	nickname → read-only → doar getter.
✅ Luptă:
•	shouldAttackOpponent(PlayerStatus opponent):
o	Simulează un duel;
o	Returnează true dacă jucătorul ar câștiga.
________________________________________
💡 Observații OOP
•	nickname e read-only → doar getter;
•	gameName → static, acces controlat;
•	Separare logică (e.g., metodă internă pentru calcul distanță);
•	Respectă incapsularea (private fields + public methods).
