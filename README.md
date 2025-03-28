
import argparse
import tasks

def main():
    parser = argparse.ArgumentParser(description="AI Manager - Task Management")
    subparsers = parser.add_subparsers(dest="command")

    # إضافة مهمة
    add_parser = subparsers.add_parser("add", help="Add a new task")
    add_parser.add_argument("task", type=str, help="Task description")

    # عرض المهام
    subparsers.add_parser("list", help="List all tasks")

    # حذف مهمة
    delete_parser = subparsers.add_parser("delete", help="Delete a task")
    delete_parser.add_argument("task_id", type=int, help="Task ID to delete")

    # تحديث مهمة
    update_parser = subparsers.add_parser("update", help="Update a task")
    update_parser.add_argument("task_id", type=int, help="Task ID to update")
    update_parser.add_argument("new_task", type=str, help="New task description")

    args = parser.parse_args()

    if args.command == "add":
        tasks.add_task(args.task)
    elif args.command == "list":
        tasks.list_tasks()
    elif args.command == "delete":
        tasks.delete_task(args.task_id)
    elif args.command == "update":
        tasks.update_task(args.task_id, args.new_task)

if __name__ == "__main__":
    tasks.create_table()  # إنشاء الجدول عند بدء التشغيل
    main()
