# Board-game-
const config = {     type: Phaser.AUTO,     width: 800,     height: 600,     scene: [BootScene, BoardScene, FightScene],     physics: { default: 'arcade', arcade: { debug: false } } };  const game = new Phaser.Game(config);  class BootScene extends Phaser.Scene {     constructor() { super('BootScene'); 
