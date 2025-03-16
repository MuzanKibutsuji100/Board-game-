const config = {
    type: Phaser.AUTO,
    width: 800,
    height: 600,
    scene: [BootScene, BoardScene, FightScene],
    physics: { default: 'arcade', arcade: { debug: false } }
};

const game = new Phaser.Game(config);

class BootScene extends Phaser.Scene {
    constructor() { super('BootScene'); }
    preload() { this.load.image('board', 'assets/monopoly_board.png'); }
    create() { this.scene.start('BoardScene'); }
}

class BoardScene extends Phaser.Scene {
    constructor() { super('BoardScene'); }
    create() {
        this.add.image(400, 300, 'board');
        this.players = [{ name: "Player 1", cash: 1500, pos: 0 }];
        this.diceButton = this.add.text(350, 500, 'Roll Dice', { fill: '#fff' })
            .setInteractive().on('pointerdown', this.rollDice, this);
    }
    rollDice() {
        let roll = Phaser.Math.Between(1, 12);
        this.players[0].pos = (this.players[0].pos + roll) % 40;
        this.checkFight();
    }
    checkFight() {
        if (this.players[0].pos % 5 === 0) { this.scene.start('FightScene'); }
    }
}

class FightScene extends Phaser.Scene {
    constructor() { super('FightScene'); }
    create() {
        this.add.text(300, 250, 'Fight Mode! Press SPACE to Attack!', { fill: '#ff0000' });
        this.input.keyboard.on('keydown-SPACE', () => this.endFight(), this);
    }
    endFight() { this.scene.start('BoardScene'); }
}
